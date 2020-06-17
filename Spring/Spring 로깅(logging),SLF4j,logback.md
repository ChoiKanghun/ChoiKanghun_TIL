

# TIL 200605(Fri)

# 스프링

<br>

## 로깅

<br>

### 개념

<br>

정보를 제공하는 일련의 기록인 로그(log)를 생성하도록 하는 활동

<br>

### 작성이유

초보 프로그래머들은 자신이 아는 분야의 적음을 극복하기 위해, 
시스템 설게자들은 시스템의 복잡성 때문에 로그를 이해하고 사용해야 한다. 

로그는 프로그램이 실행되는 중에도 작성돼야 한다. 

<br>

### 이점

<br>

로그는 버그를 고치기 위한 유용한 정보를 제공한다. 

성능에 관한 통계를 제공한다. 

 <br>

### 작성방법

<br>

`System.out.print()`을 이용할 수도 있지만, 이것은 초보들이 이용하는 방법이다. 왜냐하면 파일단위로 쓰는 것도 아니고 그냥 출력만 하기 때문.

주로 로깅 라이브러리를 이용한다. 

 <br>

### 자주 사용되는 로그 라이브러리

<br>

* java.util.logging

  http://www.vogella.com/tutorials/Logging.article.html 

  JDK 1.4부터 추가된 라이브러리이다. 

  별도로 import할 필요는 없지만 제공하는 기능이 적어 요즘엔 많이 사용하진 않는다. 

   <br>

* Apache Commons Logging

  http://commons.apache.org/proper/commons-logging/ 

  아파치 재단에서 제공하는 Commons 라이브러리에 들어있는 logging 라이브러리.

   <br>

* Log4j
  http://logging.apache.org/log4j/2.x/ 

  아파치 재단에서 제공하는 로깅 라이브러리.
  가장 성공적이고 가장 많이 쓰인다. 

   <br>

* Logback 

  https://logback.qos.ch/ 

  Seki Gulcu가 Log4j의 단점을 보완하기 위해 만든 라이브러리.

  log4j만큼 많이 쓰이진 않지만 성능은 더 좋다. 

 <br>

## SLF4J

logging관련 라이브러리는 다양하다. 이러한 라이브러리들을 통일된 방식으로 사용할 수 있도록 서비스를 제공하는 것이 SLF4J이다.  
<br>

SLF4J는 로깅 Facade이다. Facade는 [퍼사드](https://ko.wikipedia.org/w/index.php?title=퍼사드&action=edit&redlink=1)는 [클래스 라이브러리](https://ko.wikipedia.org/wiki/라이브러리) 같은 어떤 소프트웨어의 다른 커다란 코드 부분에 대한 간략화된 인터페이스를 제공하는 객체이다.
<br>

장점 : 

- 퍼사드는 [소프트웨어 라이브러리](https://ko.wikipedia.org/wiki/라이브러리)를 쉽게 사용할 수 있게 해준다. 또한 퍼사드는 [소프트웨어 라이브러리](https://ko.wikipedia.org/wiki/라이브러리)를 쉽게 이해할 수 있게 해 준다. 퍼사드는 공통적인 작업에 대해 간편한 메소드들을 제공해준다.
- 퍼사드는 라이브러리를 사용하는 코드들을 좀 더 읽기 쉽게 해준다.
- 퍼사드는 라이브러리 바깥쪽의 코드가 라이브러리의 안쪽 코드에 의존하는 일을 감소시켜준다. 대부분의 바깥쪽의 코드가 퍼사드를 이용하기 때문에 시스템을 개발하는 데 있어 유연성이 향상된다.
- 퍼사드는 좋게 작성되지 않은 API의 집합을 하나의 좋게 작성된 API로 감싸준다.

 <br>

#### SLF4J 구조

 <br>

![1](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fk.kakaocdn.net%2Fdn%2FbTpqIB%2FbtqEHwFBHi7%2Fu90jd5kouKlwzyVNioN9H1%2Fimg.png)

 <br>

구조를 살펴보면, 녹색의 application들은 SLF4J API 를 참조하고, 

API는 application의 요청에 따라 layer나 framework를 참조한다. 

이렇게 만들어두면, 더 좋은 기능을 가진 로깅  라이브러리가 나온다고 해도 applcation에서는 수정해야 할 것이 거의 없다. 

 <br>

#### Spring에서 SLF4J와 logback 사용하기.

먼저 SLF4J와 logback 라이브러리를 추가한다. 

여기서는 Maven을 통해 추가했다.

 <br>

```xml
		<dependency>
            <groupId>org.slf4j</groupId>
            <artifactId>slf4j-api</artifactId>
            <version>1.7.25</version>
        </dependency>

        <dependency>
            <groupId>ch.qos.logback</groupId>
            <artifactId>logback-classic</artifactId>
            <version>1.2.3</version>
        </dependency>

        <dependency>
            <groupId>org.slf4j</groupId>
            <artifactId>jcl-over-slf4j</artifactId>
            <version>1.7.25</version>
        </dependency>

        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-context</artifactId>
            <version>${spring.version}</version>
        </dependency>
```





 <br>

참고로 logback-classic 라이브러리는, slf4j-api ver.1.7.25에 의존성을 가지고 있다. 

따라서 logback-classic 라이브러리를 추가했다면 slf4j 라이브러리를 추가하지 않아도 자동으로 설치된다. 

Spring은 따로 로깅설정을 하지 않아도 기본적으로 commons-logging을 이용해서 로그를 남기는데, logback 라이브러리를 사용하기 위해서는 commons-logging이 사용되지 않도록 따로 설정해야 한다. 

 <br>

이를 위해서는 commons-logging 부분을 없애야 하는데, Spring 에서는 commons-logging을 찾으려고 하기 때문에 오류가 발생한다. 이 오류를 해결하기 위해서는 `jcl-over-slf4j`를 추가해주어야 한다. 

 <br>

이렇게 한다면 Spring은 commons-logging 대신 slf4j를 이용해 로그를 남기게 된다. 

그런데 실제로 로그를 남기는 것은 logback으로 해줄 것이기 때문에, 해당 부분을 추가한다.

 <br>

logback 설정 파일은 따로 있다. 이름은 logback.xml이다. 

해당 설정 파일의 루트 요소는 configuration이다. 

그리고 해당 루트 요소 안에는 appender, looger, root 등에 대한 설정을 하게 된다.  

주로 resources 폴더 안에 담아둔다. 

 <br>

logback.xml의 예 - 

 <br>

```xml
<?xml version="1.0" encoding="UTF-8"?>
<configuration scan="true" scanPeriod="30 seconds">
    <appender name="CONSOLE" class="ch.qos.logback.core.ConsoleAppender">
        <encoder>
            <Pattern>%d{HH:mm} %-5level %logger{36} - %msg%n</Pattern>
        </encoder>
    </appender>

    <appender name="FILE" class="ch.qos.logback.core.rolling.RollingFileAppender">
        <file>/tmp/access.log</file>
        <rollingPolicy class="ch.qos.logback.core.rolling.TimeBasedRollingPolicy">
            <fileNamePattern>/tmp/access-%d{yyyy-MM-dd}.log</fileNamePattern>
            <maxHistory>30</maxHistory>
        </rollingPolicy>

        <encoder>
            <Pattern>%d{HH:mm} %-5level %logger{36} - %msg%n</Pattern>
        </encoder>
    </appender>

    <logger name="org.springframework" level="info"/>
    <logger name="kr.or.connect" level="debug"/>

    <root level="debug">
        <appender-ref ref="CONSOLE"/>
        <appender-ref ref="FILE"/>
    </root>
</configuration>
```



  <br>



#### appender 

먼저 appender는 어디에다가 어떤 포맷으로 로그를 남길 것인지를 정한다. 

대표적으로는 consoleAppender, FileAppender, RollingFileAppender가 있다. 

 <br>

ConsoleAppender는 콘솔에 로그를 어떤 포맷으로 남길 것인지 정하는 것이다.

FileAppender는 파일에 로그를 어떤 포맷으로 남길 것인지 정하는 것이다. 

RollingFileAppender 의 경우에는 일단 사용목적이  로그 양이 많아질 경우에 문제가 생기는 것을 대비해 하루 단위로 로그 파일을 백업하면서 로그를 남기고자 할 때 사용한다. 당연히 이 부분에 관한 설정을 하는 게 RollingFileAppender인 거고.

<br>

**Console Appender **
<br>

ConsoleAppender의 경우 다음과 같은 형식으로 등록한다. 

```xml
<appender name = "CONSOLE" class = 
          "ch.qos.logback.core.ConsoleAppender">
	<encoder>
        <Pattern>
        	%d{HH:mm} $-5level %logger{36} - %msg%n
        </Pattern>
    </encoder>
</appender>
```

 <br>

appender 요소 안에 name은 보통 CONSOLE이라고 정한다. 

class로는 ConsoleAppender를 지정한다. 

pattern 안에 로그를 출력할 포맷을 지정한다. 

%logger는 logger의 이름을 축약해서 출력하는 부분이고, 

`{36}` 같은 부분은 length이다. 이 length는 최대 자릿수를 의미한다. 

`%-5level`은 로그 레벨을 5의 고정폭 값으로 출력하라는 것을 의미한다. 

`%msg`는 사용자가 출력한 메시지이고, %n은 줄바꿈이다. 

 <br>

**RollingFile Appender **

RollingFile Appender는 다음과 같은 형식으로 등록한다. 

 <br>

```xml
<appender name = "FILE" 
          class = "ch.qos.logback.core.rolling.RollingFileAppender">
	<file>
    	access.log
    </file>
	<rollingPolicy class =
                   "ch.qos.logback.core.rolling.TimeBasedRollingPolicy">		<fileNamePattern>
        	access-%d{yyyy-MM-dd}.log
        </fileNamePattern>
    	<maxHistory>30</maxHistory>
    </rollingPolicy>
    <encoder>
    	<Pattern>
            %d{HH:mm}%-5level %logger{36} - %msg%n
        </Pattern>
    </encoder>
</appender>
```

 <br>

appender 이름은 주로 FILE로 설정한다. 
기본적으로 기록되는 파일명은 access.log가 될 것이고, 
디렉토리 경로는 따로 설정하지 않아서 이클립스 설치 경로에 생성될 것이다. 

rollingPolicy는 하루 단위로 생성되는 로그 파일의 이름을 설정한다. 

acess-로 시작하면서 년, 월, 일에 대한 정보를 가지고 있는 로그 파일이 

최대 maxHistory개, 즉 30개 생성된다. 

30개가 넘어가면 이전의 로그 파일들은 삭제된다. 

<br>

#### 로그레벨 설정과 root 설정

 <br>

레벨에는 

trace(level 1), debug(2), info(3), warn(4), error(5) 

가 있고 뒤에 있는 게 더 심각한 오류이다. 

프로젝트를 하게 되면 어떤 오류를 어떤 방식으로 남길지를 결정하고 로그를 남기도록 한다. 

 <br>

레벨 및 루트 설정 형식은 다음과 같다.

 <br>

 ```xml
<logger name="org.springframework" level="info"/>
<logger name="kr.or.connect" level = "debug" />
<root>
	<appender-ref ref = "CONSOLE" />
    <appender-ref ref = "FILE" />
</root>
 ```

 <br>

위 코드에 대해 설명해보겠다. 

logger는 어떤 패키지 내의 클래스들에 대해 얼마 만큼의 레벨까지 로그를 남길 건지를 결정한다. 

예를 들어 위에서는 `org.springframework`로 시작하는 패키지에 속한 클래스에 대한 로그는 info 이상의 레벨 로그를 출력하라는 것이다. 즉 info, warn, error와 관련된 로그가 기록되게 된다. 

 <br>

root 태그에다 설정하는 것은 모든 대상에 CONSOLE과 FILE Appender를 적용하라는 뜻이다. 

즉, CONSOLE에도, FILE에도 로그를 찍게된다. 

 <br>

이렇게 로그 설정을 했다면 로그를 남기기 원하는 클래스에서 SLF4J 라이브러리를 이용해서 로그를 남기면 된다. 

 <br>

#### Logger 객체 선언 및 로그 출력

 <br>

로그를 남기고자 하는 클래스에서 로거 객체를 필드로 선언한다. 

형식은 다음과 같다. 

 <br>

```java
import.org.slf4j.Logger;
import org.slf4j.LoggerFactory;
...
    
private Logger logger = LoggerFactory.getLogger(this.getClass());
```

 <br>

로그 출력은 로그를 남기고 싶은 위치에서 logger가 가지고 있는 다섯 가지 메서드를 사용해 실행한다. 

 <br>

```java
logger.trace("{} {} 출력", "값1", "값2");
logger.debug("{} {} 출력", "값1", "값2");
logger.info, warn, error.. 
```

 <br>

logger를 쓰면 문자열을 결합하기 위해 '+' 연산자를 사용할 필요가 없다. 

쓰면 느려지기도 하기에 logger 메소드들의 가변인자를 활용하면 된다. 

로그로 남길 변수의 수만큼 {}로 표현하고, 뒤에 가변인자를 넣어주면 된다. 

가변인자는 C언어의 %d, %f 같은 개념을 떠올리면 이해가 쉬울 것이다. 

 <br>

### Logging 사용해보기 

 <br>

먼저 Maven을 통해 의존성을 주입한다. pom.xml에 다음의 dependecy들을 추가한다. 

 <br>

```xml
		<dependency>
            <groupId>org.slf4j</groupId>
            <artifactId>slf4j-api</artifactId>
            <version>1.7.25</version>
        </dependency>

        <dependency>
            <groupId>ch.qos.logback</groupId>
            <artifactId>logback-classic</artifactId>
            <version>1.2.3</version>
        </dependency>

        <dependency>
            <groupId>org.slf4j</groupId>
            <artifactId>jcl-over-slf4j</artifactId>
            <version>1.7.25</version>
        </dependency>

        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-context</artifactId>
            <version>${spring.version}</version>
        </dependency>
```

 <br>

pom.xml 수정 시 MAVEN update는 필수 ! 

<br>

그리고, java/resources 폴더 안에 logback.xml 파일을 하나 만들어준다. 

해당 xml 파일은 다음을 내용으로 한다. 

 <br>

```xml
<?xml version="1.0" encoding="UTF-8"?>
<configuration scan="true" scanPeriod="30 seconds">
    <appender name="CONSOLE" class="ch.qos.logback.core.ConsoleAppender">
        <encoder>
            <Pattern>%d{HH:mm} %-5level %logger{36} - %msg%n</Pattern>
        </encoder>
    </appender>

    <appender name="FILE" class="ch.qos.logback.core.rolling.RollingFileAppender">
        <file>/tmp/access.log</file>
        <rollingPolicy class="ch.qos.logback.core.rolling.TimeBasedRollingPolicy">
            <fileNamePattern>/tmp/access-%d{yyyy-MM-dd}.log</fileNamePattern>
            <maxHistory>30</maxHistory>
        </rollingPolicy>

        <encoder>
            <Pattern>%d{YYYY년 MM월 dd일 HH시 mm분 ss초.SSS} %msg%n</Pattern>
        </encoder>
    </appender>

    <logger name="org.springframework" level="info"/>
    <logger name="kr.or.connect" level="debug"/>

    <root level="debug">
        <appender-ref ref="CONSOLE"/>
        <appender-ref ref="FILE"/>
    </root>
</configuration>
```

 <br>

예시로 로그아규먼트리졸버를 마주칠 때마다 로그를 남겨보겠다.

(아규먼트리졸버가 무엇인지 몰라도 사용형식은 파악할 수 있을 것이다.)

<br>

```java
	private Logger logger = LoggerFactory.getLogger(this.getClass());
```

 <br>

먼저 위와 같은 필드를 생성해주고, 

<br>

```java
logger.error("<- 시간 , {} <- IP, {} <- request URL", clientIp, url);
```

 <br>

위와 같이 사용한다. 

전체코드는 아래와 같은데, 그냥 참고로만 보자.

 <br>

```java
public class LogInterceptor extends HandlerInterceptorAdapter {
	private Logger logger = LoggerFactory.getLogger(this.getClass());

	@Override
	public boolean preHandle(
			HttpServletRequest request, 
			HttpServletResponse response, 
			Object handler) throws Exception {
		String clientIp = request.getRemoteAddr();
		StringBuffer url = request.getRequestURL();
		logger.error("<- 시간 , {} <- IP, {} <- request URL", clientIp, url);
		return true;
	}
}
```

  <br>

기억하자. console의 pattern은 다음과 같이 지정했다.

```html
<Pattern>%d{YYYY년 MM월 dd일 HH시 mm분 ss초.SSS} %msg%n</Pattern>
```



<br>

#### 결과

<br>

실행 결과 콘솔에는 다음이 출력된다. 

 <br>

```
2020년 06월 16일 22시 09분 43초.404 <- 시간 , 0:0:0:0:0:0:0:1 <- IP, http://localhost:8080/reservationManagement/api/32/comments <- request URL
```

 <br>

또한 `logback.xml` 에서 FILE 의 file 경로를 `/tmp/access.log `로 설정해줬다.

이 정보에 따라 C://tmp에 들어가보면, 

access 라는 이름으로 파일이 하나 생성되어 있다. 

내용은 다음과 같다. 

<br>

![image-20200605173941918](C:\Users\User\AppData\Roaming\Typora\typora-user-images\image-20200605173941918.png)

  <br>

<br>

refs -

http://www.vogella.com/tutorials/Logging/article.html

http://commons.apache.org/proper/commons-logging/

http://logging.apache.org/log4j/2.x/

https://logback.qos.ch/

[https://ko.wikipedia.org/wiki/%ED%8D%BC%EC%82%AC%EB%93%9C_%ED%8C%A8%ED%84%B4](https://ko.wikipedia.org/wiki/퍼사드_패턴)

https://logback.qos.ch/

https://github.com/sonegy/how-to-use-logback

[https://www.edwith.org/boostcourse-web/lecture/16815/﻿](https://www.edwith.org/boostcourse-web/lecture/16815/)