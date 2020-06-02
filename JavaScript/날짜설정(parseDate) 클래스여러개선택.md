### JavaScript

1. JavaScript 날짜 설정(날짜 임의설정, 날짜 parse, Date parse, String to Date, String을 Date로...)

   * 예를 들어 "2020-05-31" 이라는 String을 날짜로 설정하고 싶다고 하자. 그렇다면 다음의 순서를 거쳐 변환하면 된다. 

     1. year, month, day를 parse. substr 메소드를 이용.
     2. parse한 정보를 가지고 new Date를 만들기.
        (주의! javascript의 month는 0부터 시작한다. 즉 0이 1월(January)임을 유의하자.) <br>

     * 예제

     ```java
     var stringDate = "2020-05-31";
     
     var year = stringDate.substr(0, 4); //2020
     var month = stringDate.substr(5, 2); //5
     var day = stringDate.substr(8, 2); //31
     var parsedDate = new Date(year, month - 1, day);
     var indexOfToday = parsedDate.getDay();
     var weekday = new Array(7);
     weekday[0] = "일";
     weekday[1] = "월";
     weekday[2] = "화";
     weekday[3] = "수";
     weekday[4] = "목";
     weekday[5] = "금";
     weekday[6] = "토";
     var resultDate = weekday[indexOfToday];
     
     console.log(
     	parsedDate.toLocaleDateString() + "(" + resultDate + ")"
     );
     //2020. 5. 31.(일)
     ```

     * JS에서는 따로 weekday배열을 선언하지 않아도 쓸 수 있는 날짜 배열을 제공하지 않는 듯하다.

       <br>

2. JavaScript 클래스 여러 개 선택.(두 가지 이상의 클래스 모두 가지고 있는 클래스 선택, 복수조건)

   * 자바스크립트에서는 getElementById나 querySelector로 쿼리를 선택할 수 있다. 예를 들어 "telephone" 이라는 클래스를 가진 쿼리를 선택하려면 `document.querySelector(".telephone")`과 같이 적어주면 된다. 그런데 만약 'telephone'과 'phone' 이라는 `클래스 둘 다 가지고 있는 것`을 선택하고 싶을 때는 어떻게 해야 할까? 형식은 아주 간단하다. 예제를 통해 금방 파악해보자.<br>

     ```js
     //telephone과 phone 클래스를 가지고 있는 것.
     document.querySelector(".telephone.phone");
     //telephone과 phone과 smartphone 클래스를 가지고 있는 것.
     document.querySelector(".telephone.phone.smartphone");
     ```

     <br>

   * 만약 telephone 클래스를 가지고 있으면서 div태그인 것만 선택하려면? 다음과 같이 선택한다.<br>

     ```java
     //하나인 경우
     document.querySelector("div.telephone");
     //복수인 경우
     document.querySelectorAll("div.telephone");
     ```

     <br>

   * 이번에는 telephone 클래스를 가지고 있으면서 div태그인 것 모두와, 
     phone클래스를 가지고 있으면서 p태그인 것 모두를 한꺼번에 선택해보자.
     우리가 선택한 결과는 배열로 반환된다.

     ```javascript
     document.querySelectorAll("div.telephone, p.phone");
     ```

     



##### refs -

JS : 

http://javaeleven.com/archives/91

[https://www.it-swarm.dev/ko/javascript/%EC%97%AC%EB%9F%AC-%EC%A1%B0%EA%B1%B4%EC%9D%B4%EC%9E%88%EB%8A%94-queryselectorall/1056085745/](https://www.it-swarm.dev/ko/javascript/여러-조건이있는-queryselectorall/1056085745/)

https://shxrecord.tistory.com/139