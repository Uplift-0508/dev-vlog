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
[follow these instructions](https://support.google.com/googleplay/android-developer/answer/7384423#reset)._
<!--stackedit_data:
eyJoaXN0b3J5IjpbMjMxMzExNjU0LC0yMDE2MzU1NDI3LDMyMz
AxNDEzNywtMzE5Njc1MzkwLC0xMjM1MDkzNTc4LDczMDk5ODEx
Nl19
-->