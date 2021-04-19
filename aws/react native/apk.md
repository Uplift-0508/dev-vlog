apk 생성

구글 플레이 스토어에 올리기

안드로이드는 모든 앱들이 설치하기 전에, 각자 certificate 로 전자적으로 서명되기를 요구한다.
구글 플레이 스토어를 통해 안드로이드 어플리케이션을 배포하기 위해서 release key 로 서명해야한다. 
release key 는 이후 업데이트가 있을 때 사용된다.
2017 년 이후 구글 플레이의 App signing 기능 덕분에 구글 플레이에서 자동적으로 signing release 가 가능하게 되었다. 
반면, 어플리케이션 바이너리가 구글 플레이에 업로드 되기 전에 하나의 upload key 로 서명되어야 한다. 
안드로이드 개발자 도큐먼트에 signing your application 페이지에서 이에 대해 자세히 설명한다. 
이 가이드는 간단하게 과정에 대해 다루고 javascript 번들을 패키지하기 위해 필요한 단계들을 목록화 해두었다.

upload key 생성하기

keytool 을 사용해서 private signing key 를 생성할 수 있다. 
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTU2NTM3MjMyMiwtMTM3NzcyODQzNywtMT
MwMTEyNzMyN119
-->