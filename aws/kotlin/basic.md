코틀린에서는 기본 타입을 직접적으로 제공하지 않는다. 바이트코드에서는 아마 해당되는 기본 타입을 생성하겠지만 개발자가 코드를 직접 작성할 때는 기본 타입이 아닌 클래스를 다룬다는 것을 명심해야한다. 

그러나 아래의 경우 명시적 타입 변환이 필요하지 않다.
val longSum = 3L + intVar
다행히 더하기(+) 연산자의 경우 자동으로 intVar 의 값을 long 으로 변환하고 long 리터럴에 그 값을 더한다.

코틀린도 객체 지향 프로그래밍 (OOP, Object Oriented Programming) 언어다. 

const 와 val 는 
둘 다 한번 할당되면 변경이 불가능함을 나타내지만,
const 는 컴파일 타임에 val 은 실행시간에 할당됩니다.
val 는 자바에서 final 키워드와 같은 목적으로 사용된다. 


<!--stackedit_data:
eyJoaXN0b3J5IjpbMTkxNzU1NDAzMywtMTY0NjA3MDY5MywyMD
gxNzgxNzkyLDE3MTY0OTY3ODJdfQ==
-->