# Crontab

특정 시간 또는 특정 시간 간격으로 명령어를 실행하는 스케줄러

Cron expression 은 6 개의 연속된 필드들로 구성되어 있다.

```
second (초), 
minute (분), 
hour (시), 
day of month (일), 
month (달), 
day(s) of week(요일)
```

아래와 같이 선언할 수 있다.
```
@Scheduled(cron = "* * * * * *")
```

timezone 도 아래와 같이 선언할 수 있다.
```
@Scheduled(cron="* * * * * *", zone="Europe/Istanbul")
```


구문
|syntax                          |의미|예시 | 설명                        
|-------------------------------|-----------------------------|-----------------------------|-----------------------------|
|*           |어떤 것이든 해당             |`"* * * * * *"`|항상|
|*/x           |매 x 마다 해당           |`"*/5 * * * * *"`|매 5초|
|?           |정해지지않음            |`"0 0 0 25 12 ?"`|매 12월 25일 마다


예제
|syntax                          |의미                         |
|-------------------------------|-----------------------------|
|`"0 0 * * * *"`            |매일 매시간?            |
|`"*/10 * * * * *"`            |매 10초            |
|`0 0 8-10 * * *`|매일 8:00, 9:00, 10:00|
|`"0 0/30 8-10 * * *"`            |매일 8:00, 8:30, 9:00, 9:30, 10:00            |
|`"0 0 9-17 * * MON-FRI"`            |월요일부터 금요일까지 매일 9:00, 10:00, 11:00, 12:00, 13:00, 14:00, 15:00, 16:00, 17:00            |
|`0 0 0 25 12 ?`|매년 12월 25일 00:00:00 (매 크리스마스 자정) |


@Scheduled() 가 붙은 메소드들은 표현식에 해당하는 경우에만 호출된다.
어떤 코드를 cron expression 에 해당하는 경우에만 실행하고 싶다면, annotation 안에 cron expression 를 선언하면 된다.

```
@Component
public class MyScheduler{    
    
    @Scheduled(cron="*/5 * * * * MON-FRI")
    public void doSomething() {
        // this will execute on weekdays
    }
}
```

```
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.scheduling.annotation.Scheduled;
import org.springframework.stereotype.Component;

import java.text.SimpleDateFormat;
import java.util.Date;


@Component
public class Scheduler {

    private static final Logger log = LoggerFactory.getLogger(Scheduler.class);
    private static final SimpleDateFormat dateFormat = new SimpleDateFormat("HH:mm:ss");

    @Scheduled(cron = "*/5 * * * * *")
    public void currentTime() {
        log.info("Current Time      = {}", dateFormat.format(new Date()));
    }

}
```

아래와 같이 XML 설정을 사용할 수도 있다.
```
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.stereotype.Component;

import java.text.SimpleDateFormat;
import java.util.Date;


@Component("schedulerBean")
public class Scheduler {

    private static final Logger log = LoggerFactory.getLogger(Scheduler.class);
    private static final SimpleDateFormat dateFormat = new SimpleDateFormat("HH:mm:ss");

    public void currentTime() {
        log.info("Current Time      = {}", dateFormat.format(new Date()));
    }

}  
```
```
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 
    xmlns:task="http://www.springframework.org/schema/task"
    xsi:schemaLocation="http://www.springframework.org/schema/beans 
        http://www.springframework.org/schema/beans/spring-beans-4.1.xsd
        http://www.springframework.org/schema/task 
        http://www.springframework.org/schema/task/spring-task-4.1.xsd">


    <task:scheduled-tasks scheduler="scheduledTasks">
        <task:scheduled ref="schedulerBean" method="currentTime" cron="*/5 * * * * MON-FRI" />
    </task:scheduled-tasks>

    <task:scheduler id="scheduledTasks" />

</beans>
```
[참고]
https://riptutorial.com/spring/example/21209/cron-expression
https://www.baeldung.com/cron-expressions

<!--stackedit_data:
eyJoaXN0b3J5IjpbMTI4NjQwNzQzNCwxNjUxMjQ0MzkyLDE5NT
A2MTI5NDJdfQ==
-->