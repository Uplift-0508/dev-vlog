# apk 생성

## 구글 플레이 스토어에 올리기

안드로이드는 모든 앱들이 설치하기 전에, 각자 certificate 로 전자적으로 서명되기를 요구한다.
구글 플레이 스토어를 통해 안드로이드 어플리케이션을 배포하기 위해서 release key 로 서명해야한다. 
release key 는 이후 업데이트가 있을 때 사용된다.
2017 년 이후 구글 플레이의 App signing 기능 덕분에 구글 플레이에서 자동적으로 signing release 가 가능하게 되었다. 
반면, 어플리케이션 바이너리가 구글 플레이에 업로드 되기 전에 하나의 upload key 로 서명되어야 한다. 
안드로이드 개발자 도큐먼트에 signing your application 페이지에서 이에 대해 자세히 설명한다. 
이 가이드는 간단하게 과정에 대해 다루고 javascript 번들을 패키지하기 위해 필요한 단계들을 목록화 해두었다.

## upload key 생성하기

keytool 을 사용해서 private signing key 를 생성할 수 있다. 윈도우에선 keytool 이 `C:₩ProgramFiles₩Java₩jdkx.x.x_x₩bin` 에서 실행되어야 한다. 
`keytool -genkeypair -v -storetype RKCS12 -keystore my-upload-key.keystore -alias my-key-alias -keyalg RSA -keysize 2048 -validity 10000`
이 명령은 키 저장소와 키 암호와 키 고유 이름 필드에 대한 암호를 묻는 메시지를 보여준다.
그러면 my-upload-key.keystore 라는 이름의 파일로 keystore 를 생성한다.

keystore 는 single key 를 포함하고 10000 일 동안 유효하다. alias 는 나중에 앱을 singing 할 때 사용할 이름이다. 
따라서 기록해두는 것이 좋다.

맥에서는 JDK bin 폴더의 위치가 확실하지 않다면 다음 명령으로 확인할 수 있다.
`/usr/libexec/java_home`

그 결과 아래 처럼 JDK 디렉토리를 보여준다. 
`/Library/Java/JavaVirtualMachines/jdkX.X.X-XXX.jdk/Contents/Home`

`cd /your/jdk/path` 명령어를 사용해서 해당 디렉토리로 이동하자. 그리고 아래 처럼 sudo 명령어를 함께 써서 keytool 명령어를 사용하자.
`sudo keytool -genkey -v -keystore my-upload-key.keystore -alias my-key-alias -keyalg RSA keysize 2048 -validity 10000`

keystore file 은 private 하게 유지하자. upload key 를 유실하면 별도 지침에 따라 가이드 문서를 참고한다.

## 그레들 변수 설정하기

1. `my-upload-key.keystore` 파일을 프로젝트 폴더 안에 `android/app` 디렉토리에 위치시킨다.
2. `~/.gradle/gradle.properties` 혹은 `android/gradle.properties` 파일을 수정한다. 아래 내용을 추가한다. 

```
MYAPP_UPLOAD_STORE_FILE=my-upload-key.keystore
MYAPP_UPLOAD_KEY_ALIAS=my-key-alias
MYAPP_UPLOAD_STORE_PASSWORD=*****
MYAPP_UPLOAD_KEY_PASSWORD=*****
```

이 변수들은 global gradle variables 가 될 것이다. 
이후에 앱을 sign 하기 위해서 Gradle config 내부에서 사용할 수 있다.
그런데 위 그레들 설정 파일에 패스워드를 플레인텍스트로 둘 경우 보안상의 위험이 있기 때문에 keychain 을 사용하는 것을 권장한다. https://pilloxa.gitlab.io/posts/safer-passwords-in-gradle/

## Gradle config 에 signing config 추가하기
마지막 configuration 단계는 
upload key 를 사용해서 Release builds 를 signed 되도록 셋업하는 것이다.
프로젝트 폴더 내에 있는 `android/app/build.gradle` 파일을 수정하고 signing config 를 추가한다.
```
android {
	...
	defaultConfig {...}
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
```

## release AAB (Android App Bundle) 를 생성하기

터미널에 다음을 실행한다.
```
cd android
./bradlew bundleRelease
```

Gradle 의 `bundleRelease` 는 앱을 실행시키기 위해 필요한 모든 JavaScript 를 AAB (Android App Bundle) 에 번들한다. JavaScript bundle 하는 방법을 변경할 필요가 있거나 그릴 수 있는 resources 들을 bundle 하는 방법을 변경할 필요가 있으면 (예를 들어 default 파일이나 폴더의 이름들을 변경하거나 프로젝트의 일반 구조를 변경할 때), `android/app/build.gradle` 을 살펴보고 이 변경사항들을 어떻게 반영할지 살펴본다. 

`gradle.properties` 가 `org.gradle.configureondemand=true` 를 포함하지 않도록 한다. 그러면 relase build 가 JS 와 assets 을 앱 바이너리로 번들링하는 것을 스킵하게 한다.

AAB 는 `android/app/build/outputs/bundle/release/app.aab` 아래에 생성된다. 
그러면 구글 플레이에 업로드할 준비가 된 것이다.

구글 플레이가 AAB 형식을 받아들이기 위해서, 구글 플레이에서 signing 한 앱이 구글 플레이 콘솔에서 앱에 대한 설정이 되어 있어야 한다. 구글플레이에서 App Signing 을 사용하지 않는 현재 존재하는 앱을 업데이트하기위해서는 공식문서에 migration section 을 확인하자. 

## 앱의 release build 테스트하기

플레이스토어에 release build 를 업로드하기 전에 테스트를 철저히 해야한다. 
사전에 설치했던 이전버전들은 다 삭제하고 프로젝트 루트 위치에서 아래 명령어를 사용해서 디바이스에 새로 설치해야한다.
`npx react-native run-android --variant=relase`

`--variant release` 는 위에 설명한 대로 singing 을 셋업했다면 사용할 수 있다.
모든 실행중인 bundler instance 는 종료할 수 있다. 모든 프레임워크와 JavaScript code 는 APK 의 assets 에 번들되었기 때문이다. 


<!--stackedit_data:
eyJoaXN0b3J5IjpbLTY1MzI1NjcyLC0xMzU5ODYyMDk4LC0xOD
c0NzcyMjI5LDM0NDQxOTk0NSwtNTI4MTkzNjM4LC0xMzc3NzI4
NDM3LC0xMzAxMTI3MzI3XX0=
-->