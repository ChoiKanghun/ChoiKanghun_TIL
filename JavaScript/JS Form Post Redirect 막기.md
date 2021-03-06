# TIL 200627(Sat)

# JS Form Post 리다이렉트 막기

### JavaScript에서 form 제출 시 리다이렉트 되는 것 막기.

<br>

자바스크립트에서 `form.submit()` 과 같은 방법으로 폼을 제출하는 경우가 많다. 

이때, 폼을 제출하되 제출에 대한 응답을 보여주는 페이지로 넘어가는 것을 막고 싶은 경우, `iframe`을 이용해 폼 제출을 막는다. 

<br>

예를 들면 이런 식이다. 

```javascript
var form = document.createElement("form");
form.setAttribute("charset", "UTF-8");
form.setAttribute("method", "POST");
form.setAttribute("action", "/reservationManagement/api/reservations");
document.querySelector("#footer").innerHTML += 
      "<iframe name='ifrm' style='display:none'></iframe>";
form.setAttribute("target", "ifrm");
      
```

<br>

해당 코드를 잘 살펴보면, form을 생성하고 action을 따로 설정해준 뒤, 

`display='none'`인 iframe을 어딘가에 붙여준다. 

그리고 form의 `target`을 iframe의 `name`으로 설정해주면 POST에 대한 응답이 추가해준 iframe 안으로 쏙 들어간다. 

그리고 display가 none이기 때문에 클라이언트는 아무런 변화가 없는 것처럼 보일 것이다. 

마지막으로 input 안에 들어있던 값을 초기화해주거나 페이지를 리로드하는 것으로 마무리하자. 

참고로 페이지 리로드는 `location.reload(true);` <- 해당 코드로 구현 가능하다.



