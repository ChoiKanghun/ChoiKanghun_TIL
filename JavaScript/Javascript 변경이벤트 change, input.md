# TIL 200616(Tue)

# JavaScript 변경 이벤트 (input, change)

<br>

# input

<br>

웹 코딩을 하다 보면 어떤 요소가 변경될 때마다 특정 이벤트가 발생하도록 하고 싶을 때가 있다.  

이 경우 이용할 수 있는 속성으로는 크게 두 가지가 있는데, 그것이 input과 change 속성이다. 

먼저 input 속성에 대해 알아보도록 하자 .

<br>

## 예제

<br>

다음과 같은 html이 있다고 하자. textArea 하나와 span 태그 하나가 들어 있는 코드이다. 

<br>

```html
<body>
<textarea id = "textArea" placeholder="textarea"></textarea>
<br>
<span id = "length"></span>  / 400
<br>

</body>
<script src="test.js"></script>
```

<br>

사진으로 살펴보면 

<br>

![img](https://k.kakaocdn.net/dn/3wmvF/btqEQ6InA4T/FlwWb1296KBZkFkfZTiYv0/img.png)

<br>

위와 같이 나타난다. 

이제 js에서 input 속성을 이용해보자. 

textarea에 글자가 추가될 때마다 몇 글자인지를 표시해줄 것이다. 

참고로 여기에는 `value.length`속성을 사용했다.

<br>

```javascript
var textArea = document.querySelector("#textArea");
var textLength = document.querySelector("#length");

textArea.addEventListener("input", function() {
  textLength.innerText = this.value.length;
})

```

<br>

해당 코드를 실행시켜보자. 

다음의 이미지를 잘 보면 글자가 추가될 때마다 숫자가 바뀌는 것을 볼 수 있다. 

<br>

![img2](https://k.kakaocdn.net/dn/bIiKL4/btqESWRQtaM/QV5inhVFp5AK3SkMqjJt21/img.gif)

<br>

<br>

# Change

<br>

change 속성을 textarea에 적용하면 아무것도 일어나지 않는다. 

input 속성은 사실 text를 넣을 때에만 적용시키는 것이라고 이해하면 편하다. 

그 외에는 change 속성을 이용한다.

<br>

여기서도 예제를 한 번 살펴보자

<br>

```html
<body>

checkbox<input type="checkbox" value = "click it"/>
<br>
<div id = "testDiv" style="display:none;color:red">Hello World</div>

</body>
```

<br>

위와 같은 html 코드가 있다고 할 때, 우리가 설정한 checkbox를 클릭하면 `Hello World`라는 글자를 담고 있는 div가 노출되도록 만들 것이다.  

이를 위한 js 코드는 다음과 같다. 

<br>

```javascript
var checkbox = document.querySelector("input[type=checkbox]");
var testDiv = document.querySelector("#testDiv");
checkbox.addEventListener("change", function() {
  testDiv.style.display = "block";
})

```

<br>

아래 이미지를 통해 잘 작동하는지 확인하자. 

<br>

![img3](https://k.kakaocdn.net/dn/dgtoOU/btqEQZby7bj/icx8mtJxsNrk7qYiL5vcP1/img.gif)

