# Jemeter

jMeter 는 오픈 소스 테스팅 소프트웨어이다. 100% 자바로 작성된 부하 성능 테스팅을 위한 어플리케이션이다. jMeter 는 부하 테스팅, 함수 테스팅, 성능 테스팅, regression(퇴행) 테스팅 등의 다양한 테스트들을 할 수 있도록 고안되었다. JDK5 이상에서 동작한다.

test plans, listeners, functions, 그리고 regular expressions 들을 살펴본다.

그 전에 어플리케이션 테스팅과 연관된 전문 용어들을 살펴본다.

Performance Test
: 주어진 인프라 설정에서 가능한 최고의 성능 기대치를 정한다. 어플리케이션이 상용화되기 전에 수정해야하는 게 있다면 테스팅 과정에서 초반에 알려준다.

Load Test
: 기본적으로 시스템이 작동되는 것을 전제로 최대치의 부하에서 시스템을 테스트한다.

Stress Test
: 리소스를 압도하여 시스템을 깨는 테스트이다.

## JMeter 는 무엇인가
JMeter 는 부하 테스트, 성능 기반의 비즈니스(함수형) 테스트, regression 테스트 등을 다른 프로토콜과 기술 위에서 수행할 수 있는 소프트웨어다. 
아파치 소프트웨어 재단의 Stefano Mazzocchi 는 JMeter 원년 개발자이다. 그는 Apache Tomcat project 의 성능을 테스트하기 위해 JMeter 를 만들었다. 이후에 아파치는 JMeter 를  GUI 를 개선하고 함수적인 테스팅도 가능하도록 하기위해서 새로 설계하였다. 

JMeter 는 Swing graphical API 를 사용하는 시각적 인터페이스를 제공하는 자바 데스크탑 어플리케이션이다. 따라서 JVM 을 허용하는 환경과 워크스테이션이면 어디서든 실행할 수 있다. 

**JMeter 가 지원하는 프로토콜**
-   Web − HTTP, HTTPS sites 'web 1.0' web 2.0 (ajax, flex and flex-ws-amf)
-   Web Services − SOAP / XML-RPC
-   Database via JDBC drivers
-   Directory − LDAP
-   Messaging Oriented service via JMS
-   Service − POP3, IMAP, SMTP
-   FTP Service

**JMeter 특성**
-   오픈소스 소프트웨어라 무료로 이용 가능
-  간단하고 직관적인 GUI
-  JMeter 는 다양한 서버 타입 (Web - HTTP, HTTPS, SOAP, Database - JDBC, LCAP, JMS, Mail - POP3 등)
- 플랫폼에 독립적인 툴이다. Linux/Unix 에서는 JMeter shell script 를 실행하면되고, Windows 에서는 jmeter.bat 파일을 실행시키면 된다.
- Swing 과 경량의 컴포넌트를 지원한다 (미리 컴파일된 JAR 는 javax.swing.* 패키지들을 사용한다.)
- JMeter 는 test plans 을 XML 형식으로 저장한다. 즉 텍스트 편집기를 사용해서 test plan 을 생성할 수 있다.
- 멀티 스레드 프레임워크는 다수의 스레드를 사용해 동시에 샘플링과 별개의 스레드 그룹들로 다른 함수들의 샘플링을 동시에 가능하도록 한다.
- 확장성이 좋다.
- 자동적으로 함수형의 테스팅이 가능하게 한다.

**JMeter 동작 원리**
JMeter 는 한 user 그룹이 타겟 서버에 request 를 보내도록 시뮬레이션 한다. 그리고 테이블이나 그래프 등을 통해서 타겟 서버와 어플리케이션의 성능과 기능을 보여주는 통계자료를 반환한다. 

![enter image description here](https://www.tutorialspoint.com/jmeter/images/jmeter_process.jpg)

JMeter 는 자바 프레임워크다. JDK 가 1.6 이거나 그 이상이어야 하고, 메모리와 디스크 용량, OS 가 필요하다. 

## Test Plan 
Test Plan (테스트 계획) 은 실행 중인 테스트를 위한 컨테이너로 볼 수 있다. Test Plan 은 무엇을 테스트할지와 어떻게 할지 방법을 정의한다. test plan 은 thread group 과 logic controller 와 sample-generating controllers, listeners, timers, assertions, 그리고 configuration 요소들로 구성된다. 
test plan 은 최소 1개의 thread group 을 반드시 가져야 한다.

**test plan 작성**

STEP 1 : JMeter 실행 (mac 에서 brew 로 5.4.1 설치함)
```
1063  brew install jmeter
1064  jmeter
```
JMeter 를 실행하면 초기에 2개의 노드가 있다.
Test Plan node : 실제 test plan 이 저장되는 곳
Workbench node : 실제 사용하지 않을 때 임시로 test 요소들을 저장하는 곳. 복사/붙여넣기 용도임. test plan 을 저장할 때 Workbench item 들은 함께 저장되지 않는다.

STEP 2 : Elements 추가/삭제
Elements 를 추가할 수 있다. 
![enter image description here](https://www.tutorialspoint.com/jmeter/images/adding_thread_group.jpg)

![enter image description here](https://www.tutorialspoint.com/jmeter/images/remove_element.jpg)

STEP 3 : Element 로드/저장
![enter image description here](https://www.tutorialspoint.com/jmeter/images/load_element.jpg)

STEP 4 : Tree Elements 설정
![enter image description here](https://www.tutorialspoint.com/jmeter/images/adding_thread_group.jpg)

STEP 5 : Test Plan 저장
![enter image description here](https://www.tutorialspoint.com/jmeter/images/save_test_plan.jpg)

STEP 6 : Test Plan 실행
![enter image description here](https://www.tutorialspoint.com/jmeter/images/run_test_plan.jpg)

STEP 7 : Test Plan 종료
Stop : 즉시 스레드 종료
Shutdown : 현재 일 종료되면 스레드 종료

## Test Plan Elements
JMeter Test Plan 은 Test Element 들로 구성된다. Test Plan 은 최소 1개의 Tread Group 으로 구성된다. 각 Thread Group 안에 다수의 Element 들을 (Sampler, Logic Controller, Configuration Element, Listener, Timer) 조합할 수 있다. 
각 Sampler 는 Pre-processor Element, Post-Processor Element 또는 Assertion Element 앞에 실행될 수 있다. 

### Thread Group
Thread Group Element 는 test plan 의 시작점입니다. 이름 대로 thread group element 들은 JMeter 가 테스트할 때 사용할 스레드 수를 제어한다. 또 thread 수, ramp-up(증가) time, test iteration(반복) 수를 설정할 수 있다. 
![enter image description here](https://www.tutorialspoint.com/jmeter/images/thread_group_panel.jpg)

Thread Group Panel 은 다음 구성 요소가 있다.

**Action to be taken after a Sampler error**
: 테스트 실행중에 error 가 발생하면 테스트를
- Continue : 테스트에서 다음 element 로 계속 진행
- Stop Thread : 현재 Thread 종료
- Stop Test : 테스트를 완전히 종료

**Number of Threads** 
: 서버 어플리케이션에 connection 또는 users 의 수를 시뮬레이트한다.

**Ramp-Up Period; 늘리는 기간**
: JMeter 가 모든 thread 를 실행하는 데 걸리는 시간

**Loop Count**
test 실행할 횟수

**Scheduler checkbox**
선택하면 하단에 Scheduler 설정 섹션이 나타난다. 

**Scheduler Configuratino**
test 실행 시작과 종료 시간을 설정할 수 있다.

### Controllers
JMeter 는  두 종류 (Sampler 와 Logic Controller) 의 Controller 를 가진다. 

#### Sampler
Sampler 는 JMeter 가 server 로 특정 유형의 request 들을 전송하도록 한다. 타겟 서버로 부터 페이지에 user request 를 시뮬레이트한다. 예를 들어 HTTP 서비스에 POST, GET, DELETE 를 수행해야할 경우, HTTP Request sampler 를 추가한다.

유용한 samplers :
HTTP Request
FTP Request
JDBC Request
Java Request
SOAP/XML Request
RPC Request

#### Logic Controllers
Logic Controller 는 Thread 안에 sampler 들의 처리 순서를 제어한다. Logic controller 는 child element 들로 부터 오는 request 의 순서를 변경할 수 있다. 

JMeter 가 제공하는 Logic Controller 들이다.
-   Simple Controller
-   Loop Controller
-   Once Only Controller
-   Interleave Controller
-   Random Controller
-   Random Order Controller
-   Throughput Controller
-   Runtime Controller
-   If Controller
-   While Controller
-   Switch Controller
-   ForEach Controller
-   Module Controller
-   Include Controller
-   Transaction Controller
-   Recording Controller

#### Test Fragments
Test Fragment 는 특별한 종류의 element 이고, Thread Group element 와 동등한 레벨이다. Test Fragment 는 Module Controller 또는 Include Controller 가 참조하지 않으면 실행되지 않는 다는 점에서 Thread Group 과 차이가 있다. Test Fragment 는 Test Plan 내에서 온전히 코드 재사용을 위해 사용한다. 

### Listeners
Listener 는 Sampler 들의 결과를 로그 파일에 간단한 text, tree, table, graph 형태로 보여준다. JMeter 의 Sampler 구성요소가 실행한 test case 에 대해 수집한 데이터를 시각적으로 제공한다. 

Listener 는 test 내에 어디든 추가할 수 있고, test plan 아래에 직접 추가할 수 있다. Listener 는 자신과 동등하거나 하위 레벨의 element 로 부터 데이터를 수집한다. 

JMeter 가 제공하는 Listener 들이다.
-   Sample Result Save Configuration
-   Graph Full Results
-   Graph Results
-   Spline Visualizer
-   Assertion Results
-   View Results Tree
-   Aggregate Report
-   View Results in Table
-   Simple Data Writer
-   Monitor Results
-   Distribution Graph (alpha)
-   Aggregate Graph
-   Mailer Visualizer
-   BeanShell Listener
-   Summary Report

### Timer
기본적으로 JMeter thread 는 각 sampler 사이에 pausing(멈춤) 없이 request 를 보낸다. 이것은 일반적으로 우리가 원하지 않는다. timer element 를 추가해서 각 request 사이에 시간 텀을 정의할 수 있다.

JMeter 가 제공하는 Timer 들이다.
-   Constant Timer
-   Gaussian Random Timer
-   Uniform Random Timer
-   Constant Throughput Timer
-   Synchronizing Timer
-   JSR223 Time
-   BeanShell Time
-   BSF Time
-   Poisson Random Time

### Assertions
Assertion 은 Sampler 를 사용해서 생성한 request 의 응답의 유효성을 테스트한다. 어플리케이션이 올바른 data 를 반환하는지 증명한다. assertion 이 fail 되면 강조 표시를 해준다. 

JMeter 가 제공하는 Assertion 들이다.
-   Beanshell Assertion
-   BSF Assertion
-   Compare Assertion
-   JSR223 Assertion
-   Response Assertion
-   Duration Assertion
-   Size Assertion
-   XML Assertion
-   BeanShell Assertion
-   MD5Hex Assertion
-   HTML Assertion
-   XPath Assertion
-   XML Schema Assertion

### Configuration Elements
Configuration Element 는 sampler 들이 사용할 기본값과 변수들을 생성할 수 있다. Sampler 들에 의해 request 들을 추가/수정한다. 
같은 scope 내에 위치한 sampler 들 전에 자신이 속한 scope 의 시작점에서 실행된다. 따라서 Configuration Element 는 자신이 위치한 branch 안에서만 접근할 수 있다. 

JMeter 가 제공하는 Configuration Element 들이다.
-   Counter
-   CSV Data Set Config
-   FTP Request Defaults
-   HTTP Authorization Manager
-   HTTP Cache Manager
-   HTTP Cookie Manager
-   HTTP Proxy Server
-   HTTP Request Defaults
-   HTTP Header Manager
-   Java Request Defaults
-   Keystore Configuration
-   JDBC Connection Configuration
-   Login Config Element
-   LDAP Request Defaults
-   LDAP Extended Request Defaults
-   TCP Sampler Config
-   User Defined Variables
-   Simple Config Element
-   Random Variable

### Pre-processor Elements
Pre-processor element 는 sampler 가 실행되기 바로 전에 실행된다. 일반적으로 sample request 가 실행되기 전에 설정을 수정하는데 사용한다. 또는 response test 에서 추출하지 않을 변수들을 업데이트 하기위해서 사용한다. 

JMeter 가 제공하는 Pre-processor Element 들이다.
-   HTML Link Parser
-   HTTP URL Re-writing Modifier
-   HTTP User Parameter Modifier
-   User Parameters
-   JDBC PreProcessor
-   JSR223 PreProcessor
-   RegEx User Parameters
-   BeanShell PreProcessor
-   BSF PreProcessor

### Post-processor Elements
Post-processor 는 sampler 가 실행을 종료한 후에 실행한다. 일반적으로 response data 를 처리하는데 사용한다. 예를 들어 나중에 사용할 특정 값들을 검색하는데 사용할 수 있다. 

JMeter 가 제공하는 Pre-processor Element 들이다.
-   Regular Expression Extractor
-   XPath Extractor
-   Result Status Action Handler
-   JSR223 PostProcessor
-   JDBC PostProcessor
-   BSF PostProcessor
-   CSS/JQuery Extractor
-   BeanShell PostProcessor
-   Debug PostProcessor

### Test Elements 의 실행 순서
-   Configuration elements
-   Pre-Processors
-   Timers
-   Sampler
-   Post-Processors (unless SampleResult is null)
-   Assertions (unless SampleResult is null)
-   Listeners (unless SampleResult is null)

## Web Test Plan
Thread Group 은 최소 1개 생성해야 한다. Thread Group 은 Sampler, Controller, Listener 등 같은 다른 모든 element 들의 placeholder 이다. Thread Group 을 하나 만들고 시뮬레이트할 사용자 수를 설정할 수 있다.

JMeter 에서는 모든 node element 들이 context menu 를 사용해 추가된다. 

## Database Test Plan

데이터베이스 서버를 테스트하기 위해서 간단한 test plan 을 생성해 본다. 
테스트를 위해 어떤 데이터베이스도 사용할 수 있다. 

## Webservice Test Plan

## JMS Test Plan

## Listener
Listener 는 JMeter 가 실행되는 동안 테스트 케이스에 대해서 JMeter 가 수집한 정보들에 접근하도록 해준다. listener 는 수집한 결과나 정보들을 **tree, tables, graphs, log file** 의 형태로 보여준다. 
모든 listener 들은 동일한 raw data 를 output file 에 작성한다. 

저장할 기본 설정값들은 다음 두 가지 방법으로 정의될 수 있다. 첫번째, JMeter 폴더에 /bin 안에 jmeter.properties (user.properties) 파일이 있다. 파일에서 아래 라인을 수정하는 방법이 있다.
``` jmeter.save.saveservice.output_format=```

두번째는 Config 팝업에서 수정하는 방법이 있다. 

JMeter 는 JMeter Text Logs(JTL) 를 테스트 실행 결과로 생성한다. 이는 일반적으로 JTL 파일로 부른다. 기본 확장자가 jtl 이지만 다른 확장자들도 사용 가능하다. 

다수의 테스트들이 동일한 output 파일 이름을 사용하며 실행된다면, JMeter 는 자동적으로 새로운 데이터를 파일 끝에 붙인다. 
listener 는 테스트 결과를 파일에 기록할 수 있는 반면, UI 에 기록하지 않는다. 이것은 GUI 오버헤드를 제거함으로써 데이터를 기록하는 효율적인 수단을 제공한다는 것을 의미한다. 

GUI mode 에서 테스트가 실행될 때, Simple Data Writer 라는 listener 를 사용한다. non-GUI mode 에서 테스트가 실행될 때는, -ㅣ 플래그를 데이터 파일을 생성하는데 사용한다. 

sample 들이 많다면, listener 들이 메모리를 많이 사용할 수 있다.  필요한 메모리 양을 최소화하기 위해서는 Simple Data Write with CSV format 을 사용한다. 

### CSV Log format
CSV log format 은 설정에서 어떤 데이터 아이템들이 선택되었는지에 따라 결정된다. 특정 데이터 아이템들만 이 파일에 기록된다. 아래 표의 순서는 변하지 않는다.

|Field                |Description        |Value Example    |
|----------------|---------------|-----------------------------|
|timeStamp|in milliseconds since 1/1/1970|1354223881017|
|elapsed          |in milliseconds           |1858            |
|label          |sampler label|HTTP Request|
| responseCode | e.g. 200, 404 | 200 |
| responseMessage | e.g. OK | OK |
| threadName | | Thread Group 1-1 |
| dataType | e.g. text | text |
| success | true or false | true |
|failureMessage | if any | |
| bytes | number of bytes in the sample | 34908 |
| grpThreads | number of active threads in this thread group| 1 |
| allThreads | total number of active threads in all groups | 1 |
| URL |  | http://tutorialspoint.com |
|Filename | if Save Response to File was used | |
| latency | time to first response | 132 |
| encoding |  | utf-8 |
| SampleCount | number of samples (1, unless multiple samples are aggregated) | 1 |
| ErrorCount | number of errors (0 or 1, unless multiple samples are aggregated) | 0 |
| Hostname | where the sample was generated | LaptopManisha |
| Idle Time | number of miliseconds of 'Idle' time (normally 0) | | 
|Variables | if specified | |

 ### Response Data 저장
 response data 는 필요시에 XML log 파일에 저장될 수 있다. 그러나 큰 파일들이나 이미지들은 저장할 수 있다. 이런 경우에는 Post-Processor Save_Responses_to_a_file 을 사용한다. 이는 각 샘플에 대한 새로운 파일들을 생성한다. 그리고 샘플과 파일 이름을 저장한다. 파일명은 sample log 결과에 포함된다. data 는 샘플 log 파일이 리로드될 때 필요시에 그 파일로 부터 검색된다. 


이미 저장된 파일이 있다면 Browse... 버튼을 눌러서 불러올 수 있다.
Listener 의 GUI 데이터를 png 파일로 저장할 수 있다. 

## Functions
JMeter Functions 과 User Variables
JMeter 함수들은 테스트 트리 내에 sampler 나 다른 element 의 필드를 생성할 수 있는 특별한 값이다. 

함수 호출은 다음과 같이 생겼다.
``` 
${___functionName(var1, var2, var3)}
```
_functionName 은 function 이름과 매치된다. 예를 들어 ${___threadNum}.

함수 파라미터가 컴마를 포함하면 아래 처럼 "\" 를 붙여 컴마를 escape 한다. 
``` 
${___time(EEE\, d MMM yyyy)}
```
변수는 아래와 같이 참조된다.
```
${VARIABLE}
```

함수 목록
|Function Type |Name        |Comment    |
|----------------|---------------|-----------------------------|
|Information|threadNum|Get thread number.|
|Information|samplerName|Get the sampler name (label).|
|Information|machineIP|Get the local machine IP address.|
|Information|machineName|Get the local machine name.|
|Information|time|Return current time in various formats.|
|Information|log|Log (or display) a message (and return the value).|
|Information|logn|Log (or display) a message (empty return value).|
|Input|StringFromFile|Read a line from a file.|
|Input|FileToString|Read an entire file.|
|Input|CSVRead|Read from CSV delimited file.|
|Input|XPath|Use an XPath expression to read from a file.|
|Calculation|counter|Generate an incrementing number.|
|Calculation|intSum|Add int numbers.|
|Calculation|longSum|Add long numbers.|
|Calculation|Random|Generate a random number.|
|Calculation|RandomString|Generate a random string.|
|Calculation|UUID|Generate a random type 4 UUID.|
|Scripting|BeanShell|Run a BeanShell script.|
|Scripting|javaScript|Process JavaScript (Mozilla Rhino).|
|Scripting|jexl, jexl2|Evaluate a Commons Jexl expression.|
|Properties|property|Read a property.|
|Properties|P|Read a property (shorthand method).|
|Properties|setProperty|Set a JMeter property.|
|Variables|split|Split a string into variables.|
|Variables|V|Evaluate a variable name.|
|Variables|eval|Evaluate a variable expression.|
|Variables|evalVar|Evaluate an expression stored in a variable.|
|String|regexFunction|Parse previous response using a regular expression.|
|String|escapeOroRegexpChars|Quote meta chars used by ORO regular expression.|
|String|char|Generate Unicode char values from a list of numbers.|
|String|unescape|Process strings containing Java escapes (e.g. \n & \t).|
|String|unescapeHtml|Decode HTML-encoded strings.|
|String|escapeHtml|Encode strings using HTML encoding.|
|String|TestPlanName|Return name of current test plan.|

두 종류의 함수들이 있다.
- 사용자 정의 static values (또는 variables)
- 빌트인된 함수들

- 사용자 정의 정적 값을 사용하면 테스트 트리를 컴파일하여 실행할 때 정적 값으로 대체할 변수를 정의할 수 있습니다.
- 변수들은 중첩될 수 없다. 예를 들어 ${Var${N}} 은 동작하지 않는다.
- ___V (변수) 함수 (2.2 이상 버전들) 는 ${___V(Var${N})} 이렇게 사용하는데 쓴다.
- 이 변환 타입은 함수 없이 사용 가능하다. 하지만 덜 편리하고 덜 직관적이다. 








<!--stackedit_data:
eyJoaXN0b3J5IjpbLTU0NTEwNzI3OCwtMzcwMjIxOTA3LDYxOT
U5OTUxMSwtMTY3MzI1NDgxNiw2ODg3NTY4NDcsLTc5NjQzNjMw
OSwxMjM1NzE2ODAxLC0yMTI1NTQ1OTU4LC0xMjYwMjY0NjcyLD
E2MjY4Mzc2MjUsLTM4MzY0OTMxNCwtOTY3MTY2MzI1LC0xNTE3
Njg4NzY3LC04NDE5NTk4MzQsLTEzMTcxNTgyNyw0MDYzOTY5NT
QsLTE3NjI5NDE2MjYsLTUwMTk4MTc3NiwxNjkzMTkyMDAxLC01
ODYzNDY1OTVdfQ==
-->