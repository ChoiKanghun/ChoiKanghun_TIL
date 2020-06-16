### JavaScript

1. 배열 생성방법 <br>

   ```javascript
   // 길이가 0인 배열 생성(예전 방식)
   var myArray1 = new Array();
   
   //길이 10인 예전 방식 배열 생성
   var myArray2 = new Array(10);
   
   // 길이가 0인 literal notation 방식의 배열 생성
   var myArray3 = [];
   
   // 생성과 동시에 초기화(예전 방식)
   var myArray4 = new Array(1, 2, 3,"홍길동", "아무개");
   
   // 생성과 동시에 초기화(literal notation 방식)
   var myArray5 = [1, 2, 3, "홍길동", "아무개"];
   ```

   <br>

2. 배열에 값 넣기(push)
   <br>

   ```javascript
   var arr = [ 1, 2, 3, 4 ];
   arr.push(5);
   console.log( arr ); // [ 1, 2, 3, 4, 5 ]
   ```

   <br>

3. 동적으로 form 생성하기. (form에 객체 넣기, input 이름, 값 설정. 세팅.)
   <br>

   ```javascript
   var form = document.createElement("form"); //form생성
   form.setAttribute("charset", "UTF-8");//charset설정
   form.setAttribute("method", "POST");//method설정
   form.setAttribute("action", "/reservationManagement/api/reservations");
   //POST로 어디에 보낼지 설정.
   
   var hiddenFieldProductId = document.createElement("input");
   //input 태그 하나 생성
   hiddenFieldProductId.setAttribute("type", "hidden"); //hidden으로 설정.
   hiddenFieldProductId.setAttribute("name", "productId"); //name설정
   hiddenFieldProductId.setAttribute("value", json.displayInfo.productId);
   //value 설정.
   form.appendChild(hiddenFieldProductId);//form에 추가.
   
   document.body.appendChild(form);//body에 form을 추가.
   form.submit();//form을 제출.
   ```

   <br>

4. JS 현재 시각, 날짜 구하기
   <br>
* 오늘 날짜
  
     ```javascript
     let today = new Date();   
     ```
   
     <br>
   
   * 연도, 월, 일 구하기
     <br>
   
     ```javascript
     let year = today.getFullYear(); // 년도
     let month = today.getMonth();  // 월
     let date = today.getDate();  // 날짜
     let day = today.getDay();  // 요일
     ```
   
     <br>
   
  * 시간, 분, 초, 밀리초 구하기
    <br>
  
    ```javascript
    let today = new Date();   
     
     let hours = today.getHours(); // 시
     let minutes = today.getMinutes();  // 분
     let seconds = today.getSeconds();  // 초
     let milliseconds = today.getMilliseconds(); // 밀리초
    ```
  
    <br>
  
   * 특정 형식으로 날짜 구하기
     <br>
  
     ```javascript
     let today = new Date();   
     
     document.write(today.toLocaleDateString());
     document.write(today.toLocaleTimeString());
     document.write(today.toLocaleString());
     /*
     2020. 5. 26.
     오후 3:40:29
     2020. 5. 26. 오후 3:40:29
     */
     ```
  
     <br>
  
   * JS 날짜 연산하기(년, 월)
     <br>
  
     ```javascript
     let date = new Date();
     date.setFullYear(date.getFullYear() + 1);
     //오늘로부터 1년 후.
     
     date = new Date();
     date.setFullYear(date.getFullYear() - 1);
     //오늘로부터 1년 전.
     
     date = new Date();
     date.setMonth(date.getMonth() + 1);
     //오늘로부터 한 달 후.
     ```
  
     <br>
  
   * JS 날짜 구하기(일, 요일)
  <br>
     
     ```javascript
     //일
     let date = new Date();
     var thisDay = date.getDate();
     
     //요일
     var today = new Date();
     var weekday = new Array(7);
     weekday[0] = "Sunday";
     weekday[1] = "Monday";
     weekday[2] = "Tuesday";
     weekday[3] = "Wednesday";
     weekday[4] = "Thursday";
     weekday[5] = "Friday";
     weekday[6] = "Saturday";
     
     var resultDate = weekday[today.getDay()];
  ```
     
     <br>
  

refs

Javascript<br>
https://offbyone.tistory.com/133 <br>

http://blog.302chanwoo.com/2017/08/javascript-array-method/ <br>

http://blog.naver.com/PostView.nhn?blogId=ddvp16&logNo=50169756695 - document.form.action<br>
https://www.w3schools.com/jsref/met_form_submit.asp - document.form.submit();<br>
https://www.w3schools.com/jsref/prop_form_method.asp - document.form.method<br>
https://here4you.tistory.com/87 - document.form.setAttribute, form.appendChild();<br>
https://m.blog.naver.com/PostView.nhn?blogId=whdahek&logNo=220924270812&proxyReferer=https:%2F%2Fwww.google.com%2F - javascript form 전송 시 form 안에 객체 넣기.<br>

https://hianna.tistory.com/325 - 자바스크립트 현재 날짜 구하기, toLocaleDateString, toLocaleTimeString, toLocaleString<br>
https://hianna.tistory.com/326 - 자바스크립트 날짜 더하기, 빼기<br>
https://www.w3schools.com/jsref/jsref_getday.asp - 자바스크립트 요일 구하기<br>





