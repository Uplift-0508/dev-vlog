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
액션은 앱에서 일어나는 일에 해당합니다. 

## 리듀서 (Reducer)
리듀서는 액션에 따라 어떻게 앱의 state 가 변경되어야 할지 나타낸 것입니다. 리듀서는 사이드이펙트 없이 온전히 입력에 따라 결과가 결정되는 '순수 함수' 입니다. 

리덕스에서는 스토어에 하나의 리듀서만 연결할 수 있습니다. 따라서 리듀서들을 하나의 리듀서로 합쳐서 연결합니다. 

## AsyncStorage 를 이용해 영속적인 데이터 저장
앱을 재시작하면 생성한 데이터의 state 는 사라집니다. 앱의 state 를 AsyncStorage  로 저장하면 앱 재시작과 상관없이 계속 유지될 수 있습니다. 
```
import {AsyncStorage} from 'react-native';

// 아래 두 API 는 모두 비동기임에 주의합니다.
await AsyncStorage.getItem(); 
await AsyncStorage.setItem();
```


## 요약
리덕스류의 state 관리 라이브러리 단점으로 많이 언급되는 것 중 하나는 너무 많은 보일러플레이트 코드가 앱에 추가된다는 점입니다. 

대규모 리액트 앱을 state 관리 없이 개발하다 보면 결국 state 변경 관련해 다양한 버그를 만나고 이미 구현한 컴포넌트를 수정하는 것이 어렵게 될 수 있습니다. 때문에 state 와 데이터 흐름 관리에 신경을 더 많이 써야 합니다. 
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTQ5MjU5ODk0NCwyMTIzMDMyMDkwLDk3OD
I2MDk4Ml19
-->