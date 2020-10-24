# 대규모 애플리케이션의 State 관리

## 리덕스를 사용한 State 관리
리덕스는 플럭스(Flux) 데이터 흐름 패턴과 함수형 프로그래밍 개념을 기반으로 작성되었습니다. 

앱의 state 를 예측 가능하게 하고, 관리하기 쉽게 하기 위한 라이브러리가 많이 존재합니다. 리덕스는 그중 하나입니다. 

리덕스에서 state 는 하나의 객체, 앱에 유일한 하나의 스토어로 존재합니다. 리덕스의 state 에 따라 렌더링해야하는 컴포넌트는 스토어에 연결해서 state 를 props 로 전달받을 수 있습니다. 컴포넌트는 이 state 를 직접 수정하지 못합니다. 

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTgzOTU0MDQ2Niw5NzgyNjA5ODJdfQ==
-->