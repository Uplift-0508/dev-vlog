# 구글 플레이스토어에 올리기

안드로이드는 모든 앱을 설치되기 전에 증명서로 전자 서명을 

Android requires that all apps be digitally signed with a certificate before they can be installed. In order to distribute your Android application via  [Google Play store](https://play.google.com/store)  it needs to be signed with a release key that then needs to be used for all future updates. Since 2017 it is possible for Google Play to manage signing releases automatically thanks to  [App Signing by Google Play](https://developer.android.com/studio/publish/app-signing#app-signing-google-play)  functionality. However, before your application binary is uploaded to Google Play it needs to be signed with an upload key. The  [Signing Your Applications](https://developer.android.com/tools/publishing/app-signing.html)  page on Android Developers documentation describes the topic in detail. This guide covers the process in brief, as well as lists the steps required to package the JavaScript bundle.
<!--stackedit_data:
eyJoaXN0b3J5IjpbNzk1OTg4ODc3LDczMDk5ODExNl19
-->