# 구글 플레이스토어에 올리기

안드로이드는 모든 앱을 설치되기 전에 증명서로 전자 서명을 요구한다. 구글 플레이 스토어를 통해서 안드로이드 어플리케이션을 배포하기 위해서는 release key 로 서명을 해야한다. 추후 모든 업데이트를 위해 필요하다. 2017년 부터  [App Signing by Google Play](https://developer.android.com/studio/publish/app-signing#app-signing-google-play)  기능 덕분에 Google Play 에서 서명 배포를 자동으로 관리할 수 있게 되었다. 하지만 어플리케이션 바이너리가 구글 플레이에 업로드 되기 전에 upload key 로 서명해야한다. 
안드로이드 개발자 문서에  [Signing Your Applications](https://developer.android.com/tools/publishing/app-signing.html) 페이지에 자세한 설명이 있다. 여기서는 자바스크립트 번들을 패키지화하기 위해 필요한 과정을 살펴본다.

### Generating an upload key[#](https://reactnative.dev/docs/getting-started#generating-an-upload-key "Direct link to heading")

keytool 을 사용해서 private signing key 를 생성할 수 있다. 윈도우에서는 keytool 이 `C:\Program Files\Java\jdkx.x.x_x\bin` 에서 실행되
You can generate a private signing key using  `keytool`. On Windows  `keytool`  must be run from  

$ keytool -genkeypair -v -keystore my-upload-key.keystore -alias my-key-alias -keyalg RSA  -keysize 2048  -validity 10000

Copy

This command prompts you for passwords for the keystore and key and for the Distinguished Name fields for your key. It then generates the keystore as a file called  `my-upload-key.keystore`.

The keystore contains a single key, valid for 10000 days. The alias is a name that you will use later when signing your app, so remember to take note of the alias.

On Mac, if you're not sure where your JDK bin folder is, then perform the following command to find it:

$ /usr/libexec/java_home

Copy

It will output the directory of the JDK, which will look something like this:

/Library/Java/JavaVirtualMachines/jdkX.X.X_XXX.jdk/Contents/Home

Copy

Navigate to that directory by using the command  `$ cd /your/jdk/path`  and use the keytool command with sudo permission as shown below.

$ sudo keytool -genkey -v -keystore my-upload-key.keystore -alias my-key-alias -keyalg RSA  -keysize 2048  -validity 10000

Copy

_Note: Remember to keep the keystore file private. In case you've lost upload key or it's been compromised you should  [follow these instructions](https://support.google.com/googleplay/android-developer/answer/7384423#reset)._
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTM3NjQ0ODEzMSwtMzE5Njc1MzkwLC0xMj
M1MDkzNTc4LDczMDk5ODExNl19
-->