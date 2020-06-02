#### JavaScript

1. 자바스크립트 생성자 패턴(객체, 프로토타입)

   * 객체에 함수 담는 법 :

     ```javascript
     //객체
     var StudyObj = {
       name : "최강훈",
       subject : "자바 추상클래스",
       showStudy : function(){
         console.log(this.name + "님은 다음을 학습하셔야 합니다 : " + this.subject);
       }
     }
     
     StudyObj.showStudy();
     ```

   * 함수를 통해 클래스를 선언하는 법 :
     (아래와 같이 표현하는경우 객체 하나하나의 함수가 각각 메모리를 차지함.)

     ```javascript
     //함수를 통해 클래스 만들기
     function StudyObj2(name, subject){
       this.name = name;
       this.subject = subject;
       this.showStudy = function(){
         console.log(this.name + "님은 오늘 " + this.subject + "를 공부하셔야 합니다.");
       }
     }
     
     var s1 = new StudyObj2("최강훈", "자바 추상클래스");
     s1.showStudy();
     
     var s2 = new StudyObj2("최정민", "자바스크립트 변수");
     s2.showStudy();
     
     console.log(s1.showStudy === s2.showStudy);
     
     ```

   * 클래스의 프로토타입 설정

     ```javascript
     function StudyObj3(name, subject){
       this.name = name;
       this.subject = subject;
     
     }
     StudyObj3.prototype.showStudy = function(){
       console.log(this.name + "님은 오늘 " + this.subject + "를 공부하셔야 합니다.");
     
     }
     
     var proto1 = new StudyObj3("최강훈", "자바");
     var proto2 = new StudyObj3("최정민", "자바스크립트");
     
     proto1.showStudy();
     proto2.showStudy();
     console.log(proto1.showStudy === proto2.showStudy);
     
     ```

     (프로토타입을 쓰지 않으면 객체마다 메소드를 가지기 때문에 메모리 낭비 있음 !)

2. 정규표현식 RegExp 사용법

   - 숫자 하나(\d)

     ```javascript
     var target = "asd1fawer";
     console.log(
       target.match(/\d/)[0]
     )
     // 1출력
     //결과는 배열이기 때문에 [0] 이런식으로 접근해야 함.
     ```

   - 중복된 표현식 간단히({n})

     ```javascript
     var target = "asd1234fawer";
     console.log(
       target.match(/\d\d\d\d/)[0]
     )
     //위와 밑은 같음
     console.log(
       target.match(/\d{4}/)[0]
     )
     
     ```

   - or 표현(|)

     ```javascript
     var target = "john sarah tim tom tucci emily";
     console.log(
       target.match(/stark | tucci/)[0]
     )
     // '|'는 or을 의미
     
     ```

     

   - ~이 아니어야 할 때

     ```javascript
     var target = "0123456789";
     console.log(
       target.match(/[012346789]*/)[0]
     )
     // 5라는 숫자가 들어오면 안 될 때
     // 결과는 01234만 나옴.
     
     ```

     

   - 숫자 n부터 m까지([0-9])

     ```javascript
     var target = "topw2eaaz";
     console.log(
       target.match(/[0-9]/)[0]
     )
     ```

     

   - 글자 하나 (알파벳 or 숫자 - \w)

     ```javascript
     var target = "2a_hello^^age";
     console.log(
       target.match(/\w/)
     );
     //배열 크기는 1임. 조건에 맞는 것중 가장 앞에 있는 한 글자(알파벳 or 숫자)
     console.log(
       target.match(/\w/)[1]
     );
     //undefined
     console.log(
       target.match(/\w/)[2]
     );
     //undefined
     // 둘의 결과는 같음
     
     ```

     

   - 공백(\s)

     ```javascript
     var target = "2 3r 23 w";
     console.log(
       target.match(/\d\s\d/)[0]
     );
     //'2 3'을 출력
     ```

     

   - 앞 글자가 하나 이상 있어야 할 때(+)

     ```javascript
     var target = "john doe";
     console.log(
       target.match(/joh+/)[0]
     );
     //'joh'를 출력
     console.log(
       target.match(/johnd+/)[0]
     );
     //공백이 없어서 오류 출력.
     ```

     

   - 시작 기호 그리고 .* (^ and .*)

     ```javascript
     var target = "McDonald BurgerKing LotteRia";
     console.log(
       target.match(/^Mc.*\s/)[0]
     )
     //McDonald BurgerKing을 출력.
     //Mc로 시작하는 단어. 뒤에서 첫 번째 공백을 만나기 전까지.
     //.*은 모든문자'열'을 의미함.
     //뒤에서 첫 번째 공백을 만나기 전까지 다 표현해버리기 때문에 greedy 하다고 함. 
     console.log(
       target.match(/^Bu.*/)[0]
     )
     //오류가 남. ^은 어떤 변수의 맨 처음을 의미.
     
     ```

   - lazy('?')와 greedy('*')의 개념

     ```javascript
     var target = "McDonald BurgerKing LotteRia";
     console.log(
       target.match(/^Mc.*\s/)[0]
     )
     //McDonald BurgerKing을 출력.
     //Mc로 시작하는 단어. 뒤에서 첫 번째 공백을 만나기 전까지.
     //.*은 모든문자'열'을 의미함.
     //뒤에서 첫 번째 공백을 만나기 전까지 다 표현해버리기 때문에 greedy 하다고 함.
     
     console.log(
       target.match(/^Mc.*?\s/)[0]
     )
     //BurgerKing을 출력.
     //.*은 \s 앞에 ?가 따라오는 경우 가장 가까운 space를 기준으로 삼음.
     //이를 두고 lazy하다고 함.
     ```

     

   - 앞 글자가 있거나 없거나(*)

     ```javascript
     var target = "McDonald BurgerKing LotteRia";
     console.log(
       target.match(/M*/)[0]
     )
     //M을 출력
     console.log(
       target.match(/M3*/)[0]
     )
     //M을 출력. 오류 안 남.
     
     ```

     

   - ~로 끝나야 할 때($)

     ```javascript
     var target = "McDonald BurgerKing LotteRia";
     console.log(
       target.match(/L.*Ria$/)[0]
     )
     //LotteRia 출력
     
     ```

3. Form 태그 관련 메소드

   * .preventDefault() <-> .submit()

     - 폼태그가 submit 되는 것을 막음.
     - addEventListener로 submit에 등록 가능.
     - .submit()으로 submit 가능.

   * name이 arbitraryName인 input태그를 선택하는 법.

     ```html
     <body>
     <form class="testForm" action="#" method="get">
       <input type="text" name="arbitraryName" value="daf">
     </form>
     </body>
     <script>
     document.querySelector("input[name=arbitraryName]").value = "test ok";
     </script>
     <!--이렇게 해주면 value가 test ok로 바뀜.-->
     ```

   * .test(value) 메소드
     예제 :

     ```javascript
     var target = "McDonald BurgerKing LotteRia";
     var regExpTest = RegExp('Mc*');
     var regExpTest2 = RegExp('Bur*');
     var regExpTest3 = RegExp('Cry*');
     console.log(
       regExpTest.test(target)
     )
     console.log(
       regExpTest2.test(target)
     )
     console.log(
       regExpTest3.test(target)
     )
     //결과는 순서대로 true, true, false
     
     ```

---

#### 