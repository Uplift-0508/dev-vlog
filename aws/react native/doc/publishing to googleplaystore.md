# 구글 플레이스토어에 올리기

안드로이드는 모든 앱을 설치되기 전에 증명서로 전자 서명을 요구한다. 구글 플레이 스토어를 통해서 안드로이드 어플리케이션을 배포하기 위해서는 release key 로 서명을 해야한다. 추후 모든 업데이트를 위해 필요하다. 2017년 부터  [App Signing by Google Play](https://developer.android.com/studio/publish/app-signing#app-signing-google-play)  기능 덕분에 Google Play 에서 서명 배포를 자동으로 관리할 수 있게 되었다. 하지만 어플리케이션 바이너리가 구글 플레이에 업로드 되기 전에 upload key 로 서명해야한다. 
안드로이드 개발자 문서에  [Signing Your Applications](https://developer.android.com/tools/publishing/app-signing.html) 페이지에 자세한 설명이 있다. 여기서는 자바스크립트 번들을 패키지화하기 위해 필요한 과정을 살펴본다.

### Generating an upload key[#](https://reactnative.dev/docs/getting-started#generating-an-upload-key "Direct link to heading")

keytool 을 사용해서 private signing key 를 생성할 수 있다. 윈도우에서는 keytool 이 `C:\Program Files\Java\jdkx.x.x_x\bin` 에서 실행될 수 있다. 

```
$ keytool -genkeypair -v -keystore my-upload-key.keystore -alias my-key-alias -keyalg RSA  -keysize 2048  -validity 10000
```
이 명령은 키 저장소, 키의 암호, 키의 고유 이름 필드에 대한 암호를 묻는 메시지를 표시한다. 그리고 해당 keystore 을   `my-upload-key.keystore` 란 파일로 생성한다.

keystore 은 단일 키를 포함한다. 이는 10000 일 동안 유효하다. alias 는 앱을 서명할 때 사용할 이름이다. 그래서 따로 기록해두고 기억해야한다.

맥에서는 JDK bin 폴더가 어디있는지 확신할 수 없다면, 다음 명령어를 수행한다.

```
$ /usr/libexec/java_home
```
아래처럼 JDK 디렉토리를 출력할 것이다. 

```
/Library/Java/JavaVirtualMachines/jdkX.X.X_XXX.jdk/Contents/Home
```

`$ cd /your/jdk/path` 명령어로 해당 디렉토리로 이동해서 아래 sudo keytool 명령어를 실행한다. 

```
$ sudo keytool -genkey -v -keystore my-upload-key.keystore -alias my-key-alias -keyalg RSA  -keysize 2048  -validity 10000
```
keystore file 은 private 으로 유지한다. upload key 를 분실한다면 아래 가이드를 참고한다.
[follow these instructions](https://support.google.com/googleplay/android-developer/answer/7384423#reset).


### Setting up Gradle variables[#](https://reactnative.dev/docs/getting-started#setting-up-gradle-variables "Direct link to heading")

1. `my-upload-key.keystore` 파일을 프로젝트 폴더에서 `android/app` 디렉토리 아래에 옮겨둔다.
2. `~/.gradle/gradle.properties` 파일 혹은 `android/gradle.properties` 파일을 수정한다. 아래 설정을 추가한다. (`*****` 는 실제 keystore password, alias, key password 로 대체한다)
MYAPP_UPLOAD_STORE_FILE=my-upload-key.keystore
MYAPP_UPLOAD_KEY_ALIAS=my-key-alias
MYAPP_UPLOAD_STORE_PASSWORD=*****
MYAPP_UPLOAD_KEY_PASSWORD=*****

이것은 global gradle variable 이다. 앱을 서명할 때 gradle config 로 사용할 것이다. 

보안 주의: password 를 plaintext 로 저장하지 않으면, OSX 를 실행할 수 있다.  [store your credentials in the Keychain Access app](https://pilloxa.gitlab.io/posts/safer-passwords-in-gradle/)를 참고하자. 그러면 `~/.gradle/gradle.properties` 설정에서 마지막 두 줄을 skip 할 수 있다. 

### Adding signing config to your app's Gradle config[#](https://reactnative.dev/docs/getting-started#adding-signing-config-to-your-apps-gradle-config "Direct link to heading")

마지막 설정 단계는, upload key 를 사용해서 서명하기 위한 release build 를 세팅하는 것이다.
프로젝트 폴더 내에 `android/app/build.gradle` 파일을 수정하고 서명 config 를 추가한다.

```
...
android {
    ...
    defaultConfig { ... }
    signingConfigs {
        release {
            if (project.hasProperty('MYAPP_UPLOAD_STORE_FILE')) {
                storeFile file(MYAPP_UPLOAD_STORE_FILE)
                storePassword MYAPP_UPLOAD_STORE_PASSWORD
                keyAlias MYAPP_UPLOAD_KEY_ALIAS
                keyPassword MYAPP_UPLOAD_KEY_PASSWORD
            }
        }
    }
    buildTypes {
        release {
            ...
            signingConfig signingConfigs.release
        }
    }
}
...
```

### Generating the release APK[#](https://reactnative.dev/docs/getting-started#generating-the-release-apk "Direct link to heading")

터미널에서 아래를 실행한다.
```
$ cd android
$ ./gradlew bundleRelease
```
그레들의 `bundleRelease`는 app 을 실행시키기 위해서 필요한 모든 JavaScript 를 AAB ([Android App Bundle](https://developer.android.com/guide/app-bundle))에 bundle 한다. JavaScript bundle 과/또는 리소스들을 번들하는 방법을 바꿔야한다면, (예를들어 default file/folder 이름 또는 프로젝트 구조를 변경한 경우), 이 변경사항을 반영하기 위해 `android/app/build.gradle` 을 어떻게 수정해야할지 살펴본다.

gradle.properties 는 _org.gradle.configureondemand=true (release build 가 JS 와 assets 를 앱 바이너리에 번들링하는 것을 스킵한다는 것을 의미) 를 포함하지 않는다. 

생성된 AAB 은 `android/app/build/outputs/bundle/release/app.aab` 아래에 있다. 이제 구글 플레이에 업로드할 준비가 되었다.

구글 플레이에서 AAB 포맷을 사용하기 위해서 구글 플레이에서 앱 서명은 구글 플레이 콘솔에서 어플리케이션을 위한 설정을 해야한다. 만약 구글 플레이에 의해 앱 서명을 사용하지 않은 이미 존재하는 앱을 업데이트 하려면,  [migration section](https://reactnative.dev/docs/getting-started#migrating-old-android-react-native-apps-to-use-app-signing-by-google-play)  을 참고한다. 어떻게 설정을 변경해야할지 알 수 있다. 

### Testing the release build of your app[#](https://reactnative.dev/docs/getting-started#testing-the-release-build-of-your-app "Direct link to heading")

플레이 스토어에 release build 를 업로드하기 전에 테스트를 철저히 해야한다. 이전에 설치했던 앱의 이전 버전들을 제거해야한다. 프로젝트 루트 위치에서 아래 명령어로 디바이스에 앱을 설치한다.
```
$ npx react-native run-android --variant=release
```
 `--variant=release` 은 위에 설명된 방법으로 서명을 셋팅했을 때만 사용 가능한다. 

모든 프레임워크와 자바스크립트 코드가 APK 의 asset 으로 번들되었기 때문에, 실행중인 번들러 인스턴스들을 종료할 수 있다. 

You can terminate any running bundler instances, since all your framework and JavaScript code is bundled in the APK's assets.
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTQyMDMzNzI0MCwtMTY5NzAxMzI4OSwxND
AzMjM0NDQxLC0yMDE2MzU1NDI3LDMyMzAxNDEzNywtMzE5Njc1
MzkwLC0xMjM1MDkzNTc4LDczMDk5ODExNl19
-->