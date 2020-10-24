# 대규모 애플리케이션의 State 관리

## 리덕스를 사용한 State 관리
리덕스는 플럭스(Flux) 데이터 흐름 패턴과 함수형 프로그래밍 개념을 기반으로 작성되었습니다. 

앱의 state 를 예측 가능하게 하고, 관리하기 쉽게 하기 위한 라이브러리가 많이 존재합니다. 리덕스는 그중 하나입니다. 

리덕스에서 state 는 하나의 객체, 앱에 유일한 하나의 스토어로 존재합니다. 리덕스의 state 에 따라 렌더링해야하는 컴포넌트는 스토어에 연결해서 state 를 props 로 전달받을 수 있습니다. 컴포넌트는 이 state 를 직접 수정하지 못합니다. 

state 의 변경은 미리 정의도니 액션을 통해 이루어집니다. 하나의 리듀서는 이전의 state 와 액션을 통해 받은 정보를 바탕으로 새로운 state 를 계산합니다. 결국 state 가 어떻게, 언제 변경되는지에 대한 로직은 한 곳에만 존재하기 때문에 디버깅이 편해집니다.

redux 패키지와 리덕스와 리액트를 연결해주는 react-redux 패키지도 설치해야 합니다. 

```
npm install --save redux react-redux
```

## 액션 (Action)
state 변화를 이끌어 내는 액션의 종류를 선언합니다. 
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE0MDM4MjQ2MzIsOTc4MjYwOTgyXX0=
-->