

# TIL 200604(Thu)

# JavaScript file Upload 자바스크립트 파일업로드

## 부제 : 자바스크립트 form 이미지 업로드

자바스크립트에서 form태그를 이용해 이미지를 업로드할 수 있다. 

사용방법은 다른 input 태그와 비슷하게 input type만 "file"로 주면 된다. 

확인해보자. 

 

```html
<body>
  <form name="test_form" action="index.html" method="post">
    <input type="text" name="name">
    <input type="text" name="email">
    <input type="file" name="file_image">
  </form>
</body>
```

 

이렇게 생긴 html 파일을 실행시키면, 

input text 두 개와 함께 

"file_image"라는 이름을 가진 부분이 다음과 같이 표시된다.

![image-20200604155131727](C:\Users\User\AppData\Roaming\Typora\typora-user-images\image-20200604155131727.png)

 

위 이미지에서 파일 선택을 눌러보면, 우리가 익숙하게 접해왔던 파일 업로드 창이 뜬다.

 

![image-20200604155232292](C:\Users\User\AppData\Roaming\Typora\typora-user-images\image-20200604155232292.png)

 

 

그러고 나서, '42'라는 파일을 한번 업로드 해보면,

 

![image-20200604155308696](C:\Users\User\AppData\Roaming\Typora\typora-user-images\image-20200604155308696.png)

 

위와 같이 파일이 올라간듯한 형태로 나타난다.

 

### 이미지 파일만 올라가도록 설정하기.

 

파일을 올리되 이미지 파일만 올라가도록 설정할 수도 있다. 

이렇게 설정하는 방법은 무엇인지, 또 해당 설정 외의 파일을 올리려고 하면 어떻게 되는지 살펴보자.

 

#### 형식

 

accept = "image/png, image/jpeg"



#### 예제코드

 

```html
<input type="file" name="file_image" accept="image/png, image/jpeg">
```



 위와 같이 accept라는 것에 파일의 형식을 지정해준다. 

저렇게 설정할 경우, `파일 선택` 이라는 버튼을 눌렀을 때 다음과 같이 

`사용자 지정 파일` 이라는 이름으로 png, jpeg 형식의 파일(+ 폴더)만 보여준다. 

 

![image-20200604161339645](C:\Users\User\AppData\Roaming\Typora\typora-user-images\image-20200604161339645.png)

 

> 참고로 '사용자 지정 파일' 부분을 모든 파일로 바꿔주면 다른 형식의 파일도 뜨게 된다.

  

### JavaScript로 파일 확장자, 파일 크기 제한하기.

 

JavaScript로도 파일 확장자나 파일 크기를 확인하여 파일 업로드를 제한할 수 있다. 

해당 개념에 대한 아이디어는 JavaScript로 파일이 업로드 될 때(change), 해당 파일의 확장자나 파일 크기를 검사하는 것이다.

예제를 통해 살펴보자.

 

#### 예제  

 

```javascript
//<input type="file" name="file_image" id="image">

var inputImage = document.querySelector("#image");

inputImage.addEventListener("change", function(evt){
  var image = evt.target.files[0];
  debugger;
})
```

 

위 코드와 같이 debugger를 통해 업로드 한 파일의 정보를 읽어보면, 


![image-20200604201120294](C:\Users\User\AppData\Roaming\Typora\typora-user-images\image-20200604201120294.png)

 

위 이미지와 같이  최근 수정 일자나 파일의 type, 그리고 size까지 확인할 수 있다.

 

이제, 이 정보를 가지고 들어온 파일이 이미지 파일인지 아닌지 확인해보자.

 

```javascript
var inputImage = document.querySelector("#image");

function ifImage(file){
  var validity
    = (["image/png", "image/jpg", "image/jpeg"].indexOf(file.type) > -1);

  return validity;
}

inputImage.addEventListener("change", function(evt){
  var image = evt.target.files[0];

  console.log(ifImage(image));
})
```

 

이렇게 javascript 코드를 주고, 

"~.png" 형식의 파일을 업로드 하면 true가,  

txt 파일을 업로드 하면 false가 나온다. 

이러한 속성을 이용하여 size로도 흐름을 제어할 수 있을 것이다. 

 



### 파일 제출시 주의할 점.

이제 이 파일을, 다음과 같이 생긴 버튼을 만들어 제출해보자.

 

```html
  <button type="submit">submit</button>
```

 

제출할 때 form action은 실제로 존재하지 않는 url로 줬다. 

단순한 확인만 하면 되기 때문이다. 

 

![image-20200604161701953](C:\Users\User\AppData\Roaming\Typora\typora-user-images\image-20200604161701953.png)

 

제출 후 네트워크를 확인해보면, 

`Content-Type` 은 `application/x-www-form-urlencoded`로 설정되어 있고, 

그리고 Form Data에는 name, email, file_image 정보가 나와 있다. 

 

일반적으로 `Content-Type` 은 `application/x-www-form-urlencoded`을 많이 쓴다.

그런데 (이미지)파일을 보낼 때에는 Content-type을 `multipart/form-data`로 해주는 것이 안정적이다.

설정하는 방법은 다음과 같다. 

 

#### 형식

 

enctype = multipart/form-data

 

#### 예제

 

```html
<form name="test_form" action="index.html" method="post" enctype="multipart/form-data">
```

 

