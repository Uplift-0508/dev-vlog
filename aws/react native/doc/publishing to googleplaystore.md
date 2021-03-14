# 구글 플레이스토어에 올리기

안드로이드는 모든 앱을 설치되기 전에 증명서로 전자 서명을 요구한다. 구글 플레이 스토어를 통해서 안드로이드 어플리케이션을 배포하기 위해서는 release key 로 서명을 해야한다. 추후 모든 업데이트를 위해 필요하다. 2017년 부터  [App Signing by Google Play](https://developer.android.com/studio/publish/app-signing#app-signing-google-play)  기능 덕분에 Google Play 에서 서명 배포를 자동으로 관리할 수 있게 되었다. 하지만 어플리케이션 바이너리가 구글 플레이에 업로드 되기 전에 upload key 로 서명해야한다. 
안드로이드 개발자 문서에  [Signing Your Applications](https://developer.android.com/tools/publishing/app-signing.html) 페이지에 자세한 설명이 있다. 여기서는 자바스크립트 번들을 패키지화하기 위해 필요한 과정을 살펴본다.


<!--stackedit_data:
eyJoaXN0b3J5IjpbMTQ5NzM1Nzg2MiwtMTIzNTA5MzU3OCw3Mz
A5OTgxMTZdfQ==
-->