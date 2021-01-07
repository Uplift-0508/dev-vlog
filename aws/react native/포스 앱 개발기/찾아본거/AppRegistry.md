리액트 프로젝트를  create react native app 으로 생성하니 가장 최상위단의 index.js 에 기본으로 있는 코드가
``
AppRegistry.registerComponent('Appname', () => App)
``

이였다. 문득 궁금해졌다. 이건 무슨 기능일까?

AppRegistry 는 JS 앤트리 포인트이다. 모든 리액트 네이티브 앱들을 실행시키는.
App 의 root 컴포넌트들은 그들 스스로를 등록시키는데 AppRegistry.registerComponent 를 사용한다.
그러면 native 시스템은 앱 번들을 로드할 수 있다. 그다음 실제로 앱을 실행시킨다. AppRegistry.runApplication 을 호출해서.

view 가 소멸될때 앱을 종료하기 위해서는 AppRegistry.unmountApplicationComponentAtRootTag 를 호출합니다. runApplication 에 넘겨진 태그와 같이! 둘은 한 쌍이다.

AppRegistry 가 초기에 필요하다. require 시퀀스안
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE4MTM3ODQyNzIsMTYxNTc4NzIwXX0=
-->