리액트 프로젝트를  create react native app 으로 생성하니 가장 최상위단의 index.js 에 기본으로 있는 코드가
``
AppRegistry.registerComponent('Appname', () => App)
``

이였다. 문득 궁금해졌다. 이건 무슨 기능일까?

AppRegistry 는 JS 앤트리 포인트이다. 모든 리액트 네이티브 앱들을 실행시키는.
App 의 root 컴포넌트들은 그들 스스로를 등록시키는데 AppRegistry.registerComponent 를 사용한다.
그러면 native 시스템은 앱 번들을 로드할 수 있다. 그다음 실제로 앱을 실행시킨다. AppRegistry.runApplication 을 호출해서.

view 가 소멸될때 앱을 종료하기 위해서는 AppRegistry.unmountApplicationComponentAtRootTag 를 호출합니다. runApplication 에 넘겨진 태그와 같이! 둘은 한 쌍이다.

AppRegistry 가 require 시퀀스의 초기에 필요하다. JS 실행 환경이 셋업된 것을 확실히 하기 위해서. 다른 모듈들이 필요로 하기 전에.


앱 개발에서 가장 중요한건
스크롤 성능, 메모리 효율성, UI 응답성, 앱 시작 시간인것 같다!
성능 테스트는 어떻게 할까?
테스트 코드는 어떻게 짤까?
렌더링 효율이 중요한것 같다.

shadow thread 가 뭐지?

프로파일링 툴들을 만들면서 무엇이 성능을 결정하는지 알면 좋을 뜻

javascript 에서는 스레드 관리가 어떻게 되는지 알면 좋을 듯

리액트/리액트네이티브에서는 스레드 관리가 어떻게 되는지
화면을 그릴때 스레드는 어떻게 작동할지.

프론트에서는 캐시가 어떤 종류가 있고 어떻게 사용할지.

전체적으로 리액트 네이티브는 화면을 어떤 프로세스로 그릴지.

프로파일링 도구 사용하는 법, 도구들 익히기.
앱에도 그런게 있나? 성능 측정도구


한번은 날잡고 단축키 공부좀 해야할듯..

네이게이션은 날잡고 세가지 종류 정리해도 좋을듯
<!--stackedit_data:
eyJoaXN0b3J5IjpbNDI4MzcwODEwLDIwNDA1OTA2MjMsMTg5MD
YxMzMxNSw1MDY5MjQ2MTYsLTE2MjMwNzg5NTMsMTYxMzI1NzA0
Nyw1MDQzMzA4NjUsMTYxNTc4NzIwXX0=
-->