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
그레들의 `bundleRelease`는 app 을 실행시키기 위해서 필요한 모든 JavaScript 를 AAB ([Android App Bundle](https://developer.android.com/guide/app-bundle))에 bundle 한다. 
If you need to change the way the JavaScript bundle and/or drawable resources are bundled (e.g. if you changed the default file/folder names or the general structure of the project), have a look at  `android/app/build.gradle`  to see how you can update it to reflect these changes.

> Note: Make sure gradle.properties does not include  _org.gradle.configureondemand=true_  as that will make the release build skip bundling JS and assets into the app binary.

The generated AAB can be found under  `android/app/build/outputs/bundle/release/app.aab`, and is ready to be uploaded to Google Play.

_Note: In order for Google Play to accept AAB format the App Signing by Google Play needs to be configured for your application on the Google Play Console. If you are updating an existing app that doesn't use App Signing by Google Play, please check our  [migration section](https://reactnative.dev/docs/getting-started#migrating-old-android-react-native-apps-to-use-app-signing-by-google-play)  to learn how to perform that configuration change._
<!--stackedit_data:
eyJoaXN0b3J5IjpbNjc3NzU4NTI5LDE0MDMyMzQ0NDEsLTIwMT
YzNTU0MjcsMzIzMDE0MTM3LC0zMTk2NzUzOTAsLTEyMzUwOTM1
NzgsNzMwOTk4MTE2XX0=
-->