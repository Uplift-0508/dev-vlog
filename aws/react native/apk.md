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

그레들 변수 설정하기

1. my-upload-key.keystore 파일을 프로젝트 폴더 안에 android/app 디렉토리에 위치시킨다.
2. 

<!--stackedit_data:
eyJoaXN0b3J5IjpbMTU2Nzg5NDg4NiwtMTM3NzcyODQzNywtMT
MwMTEyNzMyN119
-->