코틀린에서는 기본 타입을 직접적으로 제공하지 않는다. 바이트코드에서는 아마 해당되는 기본 타입을 생성하겠지만 개발자가 코드를 직접 작성할 때는 기본 타입이 아닌 클래스를 다룬다는 것을 명심해야한다. 

그러나 아래의 경우 명시적 타입 변환이 필요하지 않다.
val longSum = 3L + intVar
다행히 더하기(+) 연산자의 경우 자동으로 intVar 의 값을 long 으로 변환하고 long 리터럴에 그 값을 더한다.

코틀린도 객체 지향 프로그래밍 (OOP, Object Oriented Programming) 언어다. 

const 와 val 는 
둘 다 한번 할당되면 변경이 불가능함을 나타내지만,
const 는 컴파일 타임에 val 은 실행시간에 할당됩니다.
val 는 자바에서 final 키워드와 같은 목적으로 사용된다. 

코틀린에서 val 은 키워드지만 const 는 private, inline 등과 같은 변경자임에 유의해야한다. const 가 val 키워드를 대체하는 것이 아니라 반드시 같이 사용되어야 한다.

**코루틴 (Coroutine)**
동시성 코드를 마치 동기 코드처럼 작성할 수 있게 해주는 기술
콜백 메소드 또는 리액티브 스트림과 같은 다른 방법들보다 훨씬 쉽게 동시적 코드를 작성할 수 있다. 

**runBlocking 함수** 는 현재 스레드를 블록하고 모든 내부 코루틴이 종료될 때까지 블록한다. runBlocking 함수 시그니처는 다음과 같다.
``
fun <T> runBlocking(block: suspend CoroutineScope.() -> T): T
``
runBlocking 함수는 인자로 CoroutineScope 에 확장 함수로 추가될 suspend 함수를 받아서 실행한뒤 그 반환값을 리턴한다.

**launch 빌더**
독립된 프로세스를 실행하는 코루틴을 시작하고, 해당 코루틴에서 리턴값을 받을 필요가 없을 때 lauch 코루틴 빌더를 사용한다. 
launch 함수 시그니처는 다음과 같다.
``
fun CoroutineScope.lauch(
	context: Coroutinecontext = EmptyCoroutineContext,
	start: CoroutineStart = CoroutineStart.DEFALUT,
	block: suspend CoroutineScope.() -> Unit
): Job
``

**Nothing 클래스**
모든 타입의 하위 타입.

**함수형 프로그래밍**
불변성 (immutability) 를 선호하고, 
순수함수를 사용하는 경우에
동시성을 쉽게 구현할 수 있으며,
반복보다는 변형 (transformation) 을 사용하고,
조건문보다는 필터를 사용하는 
코딩 스타일을 지칭한다.

**컬렉션**
코틀린은 자바와 다르게 중개자 역할을 하는 스트림을 거치지 않고 
다양한 메소드를 컬렉션 클래스에 직접 추가한다.


<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE0NTczMjYyNCwzNjg1MzM5MjUsLTE2ND
Q1MjcyMzYsMTI0NDIxMTk1LDY5NTQ0MTgxMiwtMTkxNzcwOTk5
NiwtMTEzOTY3NTM0NSwtMTQ4MDE3MDk2NywxOTE3NTU0MDMzLC
0xNjQ2MDcwNjkzLDIwODE3ODE3OTIsMTcxNjQ5Njc4Ml19
-->