# 구글 플레이스토어에 올리기

안드로이드는 모든 앱을 설치되기 전에 증명서로 전자 서명을 요구한다. 구글 플레이 스토어를 통해서 안드로이드 어플리케이션을 배포하기 위해서는 release key 로 서명을 해야한다. 추후 모든 업데이트를 위해 필요하다. 2017년 부터  [App Signing by Google Play](https://developer.android.com/studio/publish/app-signing#app-signing-google-play)  덕분에 Google Play 에서 서명 배포를 자동으로 관리할 수 있게 되었다. 
Since 2017 it is possible for Google Play to manage signing releases automatically thanks to functionality. However, before your application binary is uploaded to Google Play it needs to be signed with an upload key. The  [Signing Your Applications](https://developer.android.com/tools/publishing/app-signing.html)  page on Android Developers documentation describes the topic in detail. This guide covers the process in brief, as well as lists the steps required to package the JavaScript bundle.
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEwNjk3MTc1NTQsLTEyMzUwOTM1NzgsNz
MwOTk4MTE2XX0=
-->