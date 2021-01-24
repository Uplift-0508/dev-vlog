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

|                |syntax                          |HTML                         |
|----------------|-------------------------------|-----------------------------|
|Single backticks|`'Isn't this fun?'`            |'Isn't this fun?'            |
|Quotes          |`"Isn't this fun?"`            |"Isn't this fun?"            |
|Dashes          |`-- is en-dash, --- is em-dash`|-- is en-dash, --- is em-dash|

[참고]
https://riptutorial.com/spring/example/21209/cron-expression
<!--stackedit_data:
eyJoaXN0b3J5IjpbMzI3NDk3NDAyXX0=
-->