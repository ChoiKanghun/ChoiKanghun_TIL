# TIL 200529, 200530(Fri, Sat)

### 영어

1. 단어
   - complimentary sample : 무료 샘플
   - come up with : 제안하다.
   - move : vt, vi 모두 다 됨.
   - in regard to : ~에 대한
   - interruption : 중단
   - commission : (계약 시)수수료
   - flat fee : 고정 수수료(고정 임금)
   - aside from : ~을 제외하고
   - in regard to : ~에 대한
   - credit : v. 공로를 인정하다.
   - track record : 실적
   - curlinary : 요리의
2. 문법
   - all, (a) few는 복수 <-> each는 단수



### 알고리즘

#### 	검색 알고리즘

1. 어떤 검색 알고리즘을 선택할까.

   검색에도 여러 가지 기법이 있고, 그에 따른 알고리즘이 있다. 대표적인 검색 `기법`으로는 다음의 3가지가 있다.

   * 배열 검색
   * 선형 리스트 검색
   * 이진트리 검색

   <br>

   이러한 기법들은 다시 여러 알고리즘을 적용하여 크게 세 가지 갈래로 나뉜다. 이러한 `알고리즘`의 갈래로는 다음의 세 가지가 있다.

   * 선형 검색 : 하나의 선 위에 무작위로 늘어놓은 데이터 모임에서 검색을 수행.

   * 이진 검색 : 일정한 규칙으로 늘어놓은 데이터 그룹에서 아주 빠른 검색을 수행.

   * 해시법 : 추가, 삭제가 자주 일어나는 데이터 모임에서 빠른 검색을 수행.

     - 체인법 : 같은 해시 값의 데이터를 선형 리스트로 연결 

     - 오픈 주소법 : 데이터를 위한 해시 값이 충돌할 때 다시 해시하는 법.

       <br>

   이 중 어떤 알고리즘을 선택하여 쓸 것이냐는 검색의 목적에 따라 달라진다. 검색 그 자체가 목적이라면 계산 시간이 짧은 것을 선택하면 된다. 반대로 검색과 함께 데이터의 추가, 수정이 자주 일어난다면 계산이 빨라도 데이터 추가나 수정에 많은 비용이 들어가는 알고리즘은 피해야 한다.

   <br>

   예를 들어 학생들의 번호순서대로 배열을 만들어 놓았다고 가정하자. 그렇다면 어떤 학생의 번호만 알면 검색은 매우 빠르게 일어난다. 그러나 데이터를 추가하기 위해서는 해당 학생이 몇 번째에 위치해야 하는지 알아낸 뒤에 해당 번호 뒤로 한 칸씩 모두 밀어낸 다음 해당 위치에 데이터를 추가할 수 있다. 이런 것이 검색은 빠르지만 데이 터 추가에 요구되는 비용이 많이 드는 경우다.

<br>

2. 배열검색

   * 선형검색 :
      요소가 직선 모양으로 늘어선 배열에서의 검색. 원하는 키를 만날 때까지 순서대로 검색하면 됨. 이것을 선형검색(또는 순차검색)이라고 함. 

     * 일반적인 선형 검색 :

       ```java
       static int seqSearch(int[] arr, int n, int key) {
       
       	while (true){
          	 	if (i == n)
           	    return (-1);
          		if (arr[i] == key)
              	 	return i;
       		i++;
       	}
       }
       ```

     <br>

   * 보초법 :

     일반적인 선형 검색은 while문 안에서 다음의 두 가지 상황을 모두 판단해야 한다.

     * 배열의 i번째 요소가 key인지.
     * 배열이 끝(n)을 만났는지.

     이러한 두 가지 조건 중 배열이 끝을 만났는지를 판단하는 조건은 보초법을 통해 없앨 수 있다.

     <br>

     예를 들어 배열이 10칸짜리 이고 0 ~ 9까지의 숫자가 들어가 있다고 해보자. 그렇다면 내가 '10'이라는 숫자를 찾고싶다고 할 때 while문은 한번 돌 때마다 if를 두번 만나야 한다. 그러나 미리 10이라는 숫자를 배열의 마지막에 넣고 시작한다면? 이 경우 while문 안에는 if가 딱 한번 들어가는 것으로 족하다. 예를 보자.

     ```java
     int i = 0;
     arr[n] = key;
     
     while (true){
         if (a[i] == key)
             break;
         i++;
     }
     
     return (i == n) ? -1 : i;
     ```

     <br>

### JavaScript

1.  JavaScript 날짜 설정(날짜 임의설정, 날짜 parse, Date parse, String to Date, String을 Date로...)

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

     

