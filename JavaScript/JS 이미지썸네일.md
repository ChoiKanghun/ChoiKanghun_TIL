# TIL 200605(Fri)

# 자바스크립트 - 이미지 썸네일

이미지를 올리고 나면, 사용자가 올린 이미지가 어떤 것인지 썸네일을 통해 확인시켜주는 경험이 있을 것이다. 

이렇게 썸네일 띄우는 자바스크립트로 구현해보자 . 

구현을 위해서 createObjectURL을 이용하여 화면에 image 정보를 출력한다. 

 

html 

 

```html
<body>
  <form name="test_form" action="http://localhost:8080/reservationManagement/mainpage" method="GET" enctype="multipart/form-data">
    <input type="text" name="name">
    <input type="text" name="email">
    <input type="file" id = "image" name="file_image" accept="image/jpeg, image/png">
    <button type="submit">submit</button>
  </form>

   <img class="thumb_img" src= "" width="130">
</body>
```



 

javascript 

```javascript
var inputImage = document.querySelector("#image");

inputImage.addEventListener("change", function(evt){
  var image = evt.target.files[0];
  
  var elImage = document.querySelector(".thumb_img");
  elImage.src = window.URL.createObjectURL(image);
})
```

 

결과

 

![image-20200605131750753](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fk.kakaocdn.net%2Fdn%2F2eT0u%2FbtqEFK6u3Du%2FymGdv7mGmAbIv932wwD5nK%2Fimg.png)

 



window의 URL이 가지고 있는 createObjectURL의 인자로 image라는 것을 주면 썸네일을 출력할 수 있는 듯하다.

그렇다면 인자로 들어온 image는 무엇일까?

 

console.log(image.type);

console.log(image);

 

를 찍어보자. 

 

![image-20200605131939352](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fk.kakaocdn.net%2Fdn%2FIR0lW%2FbtqEGhP63EA%2FWQjYrnC72BckI2SNkiM3h0%2Fimg.png)

 

아하. object를 인자로 받고, 해당 object는 file이구나.

MDN 문서를 살펴보면 인자로 다음의 세 가지를 받을 수 있다고 한다. 

 

매개변수

- `object`

  객체 URL을 생성할 [`File`](https://developer.mozilla.org/ko/docs/Web/API/File), [`Blob`](https://developer.mozilla.org/ko/docs/Web/API/Blob), [`MediaSource`](https://developer.mozilla.org/ko/docs/Web/API/MediaSource) 객체.

  



refs - 

https://developer.mozilla.org/ko/docs/Web/API/URL/createObjectURL

