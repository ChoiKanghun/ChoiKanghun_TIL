### MYSQL

#### INSERT

INSERT (INTO)를 사용하여 테이블에 새로운 레코드를 추가할 수 있다.



#### 테이블에 레코드 추가하기

다음과 같은 문법을 통해 테이블에 새로운 레코드를 추가할 수 있다.

##### 문법

1. INSERT INTO 테이블이름(필드1, 필드2, 필드3, ...)

  VALUES (값1, 값2, 값3, ...)

2. INSERT INTO 테이블이름

  VALUES (값1, 값2, 값3, ...)

 

INSERT INTO 옆에 필드를 명시해줌으로써 원하는 필드에만 값을 넣을 수 있다. 그리고 두 번째 문법처럼 필드의 이름을 생략할 수도 있다. 이 경우 데이터베이스의 스키마 열과 같은 순서대로 값이 할당된다.



INSERT INTO를 할 때 생략할 수 있는 필드는 다음과 같다.

 

1. NULL을 저장할 수 있도록 설정된 필드

2. DEFAULT 제약 조건이 설정된 필드

3. AUTO_INCREMENT 키워드가 설정된 필드

 

다음은 reservation 테이블에 새로운 레코드를 추가하는 예제다.

##### 예제

 

INSERT INTO reservation_info(name, telephone, email)

VALUES('최강훈', '010-2222-2222', 'rkdgns4562@naver.com');

 



#### UPDATE

UPDATE 문을 사용하여 테이블의 레코드를 수정해보자.

##### 문법

UPDATE 테이블이름

SET 필드1=값1, 필드2=값2 

WHERE 조건

<br>

UPDATE 문은 테이블에서 WHERE 절의 조건을 만족하는 레코드만 수정한다.

다음은 reservation_info 테이블의 레코드 중  id가 38인 cancel_flag를 true로 바꿔주는 예제다.

<br>

##### 예제

 

UPDATE reservation_info 

SET cancel_flag = true 

WHERE id = 38;

<br>

#### DELETE

DELETE 문을 이용하여 테이블의 레코드를 삭제해보자.

<br>

##### 문법

DELETE FROM 테이블이름

WHERE 필드이름=데이터값

<br>

DELETE 문은 테이블에서 WHERE 절의 조건을 만족하는 레코드만을 삭제한다.

 

`주의! : WHERE 절을 생략하면, 해당 테이블에 저장된 모든 데이터가 삭제된다.`

##### 다음과 같이 실행하지 않도록 주의!

DELETE FROM 테이블이름;

 

다음은 reservation_info_id가 38인 레코드만 삭제하는 예제다.

##### 예제 

 

DELETE 

FROM reservation_info_price 

WHERE reservation_info_id = 38 

 



#### SELECT

SELECT 문을 사용하여 테이블의 레코드를 선택할 수 있다.

##### 문법

SELECT 필드1, 필드2, 필드3, ...

FROM 테이블이름

[옵션: WHERE 조건]

 

다음 예제는 reservation_info 테이블의 모든 필드를 선택하는 예제이다.

#####  

##### 예제

 

SELECT name, telephone

FROM reservation_info;

 

FROM 뒤에는 레코드를 가져올 테이블명을 적어준다.

해당 테이블에서 가져올 필드들을 SELECT 뒤에 적어주면 된다.

이때 WHERE 절을 사용하여 조건을 걸 수 있다.

<br>



#### 테이블 내 모든 필드 가져오기

SELECT 에 별표(*) 기호를 사용하면, 해당 테이블의 모든 필드를 가져올 수 있다.

##### 문법

SELECT *

FROM 테이블이름

 

이러한 방식은 해당 테이블의 '모든 필드'를 선택해야 할 경우에 사용한다.

 

다음 예제는 reservation_info 테이블의 모든 필드를 선택하는 예제이다.

##### 예제

 

SELECT *

FROM reservation_info;

 





refs-

##### MYSQL

http://tcpschool.com/mysql/mysql_basic_insert

http://tcpschool.com/mysql/mysql_basic_select

http://tcpschool.com/mysql/mysql_basic_delete

http://tcpschool.com/mysql/mysql_basic_update

