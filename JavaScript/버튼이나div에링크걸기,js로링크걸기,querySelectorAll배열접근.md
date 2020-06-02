### JavaScript

자바스크립트에서 Button(또는 div)에 링크 걸기.

자바스크립트에서 html 내 button 태그에 이벤트 리스너를 통해 링크 거는 법에 대해 한참을 찾다가 결국 알아내지 못하고 혼자 시도해보다 어떻게 하는 지 알게 됐다.

먼저 일반적으로 button(div)에 링크 거는 법 ->

- html :

  ```html
  <button ... onclick = "linkMethod()">
      click it!
  </button>
  ```

- Js:

  ```java
  function linkMethod(){
      location.href = "reserve.html";
  }
  ```

---

다음으로 이벤트 리스너를 통하여 링크 거는 법.

* html :

  ```html
  <button id = "btn" onclick="">
      click it!
  </button>
  ```

* Js:

  ```java
  function testFunction(){
      document.querySelector("#btn").addEventListener('click', function(){
      	location.href = "reserve?id=" + getParamValueFromUrl("id");
      });
  }
  ```

나와 비슷한 상황이 얼마나 있겠냐 만은 나는 반드시 

```javascript
window.addEventListener("DOMContentLoaded", function(){

모든 js코드;

}
```

위와 같이 되어야 했기에 꼭 event Listener로 이벤트를 발생시켜야 했다.



### querySelectorAll 배열 접근

* querySelectorAll(".classes")[0].querySelector(".firstClassChild");
  -> 위와 같은 형태로도 접근이 가능.