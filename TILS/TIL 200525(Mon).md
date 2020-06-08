# TIL 200525(Mon)

### JavaScript

1. 정규표현식(핸드폰 번호, 이메일)

   * 핸드폰 번호 정규표현식 사용법

     ```javascript
     var regExpTel = /^\d{3}-\d{3,4}-\d{4}$/;
     ```

     사용예제 :

     ```java
     var regExpTel = /^\d{3}-\d{3,4}-\d{4}$/;
     var warningMessage = this.parentElement.querySelector("#tel_warning");
     
     if (this.value != "" && !regExpTel.test(this.value)){
     	warningMessage.style.display = "inline-block";
         ...
     ```

     ---

   * 이메일 정규표현식 사용법

     ```javascript
     var regExpEmail 
     = /^[0-9a-zA-Z]([-_.]?[0-9a-zA-Z])*@[0-9a-zA-Z]([-_.]?[0-9a-zA-Z])*.[a-zA-Z]{2,3}$/i;
     ```

     사용예제 :

     ```javascript
     var email = document.querySelector("#email");
     email.addEventListener("mouseleave", function() {
           var regExpEmail = /^[0-9a-zA-Z]([-_.]?[0-9a-zA-Z])*@[0-9a-zA-Z]([-_.]?[0-9a-zA-Z])*.[a-zA-Z]{2,3}$/i;
           var warningMessage = this.parentElement.querySelector("#email_warning");
     
           if (this.value != "" && !regExpEmail.test(this.value)) {
             warningMessage.style.display = "inline-block";
             ...
     ```

     ---

2. 정규표현식(숫자를 금액처럼 만들기)

   * 함수를 이용해 숫자를 금액처럼 만들기

     ```javascript
     //값에 콤마(,)를 더해줌. ex) 10000->10,000
     function addCommas(val){
     	return val.toString().replace(/\B(?=(\d{3})+(?!\d))/g,",");
     }
     ```

     사용예제 :

     ```javascript
     var parseNumberTotalItemPrice = Number(totalItemPrice.innerText.replace(/,/g,""));
     totalItemPrice.innerText 
         = addCommas(parseNumberTotalItemPrice + parseNumberItemPrice);
     ```

     

3. 클래스 추가, 삭제, 토글, has class
   classList - add, remove, contains, toggle

   * 클래스 추가 :

     ```javascript
     var test = document.querySelector("#test");
     
     test.classList.add("open");
     //test id를 가진 태그에 open 클래스가 추가됨.
     ```

   * 클래스 삭제

     ```javascript
     var test = document.querySelector("#test");
     
     test.classList.remove("open");
     //test id를 가진 태그의 클래스에서 open이 삭제됨.
     ```

   * 클래스를 가지고 있는지.(has class)

     ```javascript
     var test = document.querySelector("#test");
     
     test.classList.contains("open");
     //test id를 가진 클래스가 open 클래스를 가지고 있으면 true, 아니면 false
     ```

   * 토글(클래스가 있으면 삭제, 없으면 추가)

     ```javascript
     var test = document.querySelector("#test");
     
     test.classList.toggle("open");
     //test id를 가진 클래스가 open 클래스를 가지고 있으면 삭제, 없으면 추가.
     ```

4. 마우스 이벤트, 마우스 벗어날 때

   * 마우스가 현재 가리키는 DOM에서 벗어나는 경우(mouseleave)

     ```javascript
     var tel = document.querySelector("#tel");
     	  
     tel.addEventListener("mouseleave", function(){
        ...
     ```

     example gif : (마우스가 해당 영역을 벗어나면 메시지가 뜨는 이벤트 발생.)

     ![Honeycam 2020-05-25 20-45-46](C:\Users\User\Desktop\TodayILearned\img\Honeycam 2020-05-25 20-45-46.gif)

     * 더 많은 마우스 이벤트 링크 : https://steemit.com/javascript/@noreco/2dgssu