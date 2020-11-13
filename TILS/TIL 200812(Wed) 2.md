

# TIL 200812(Wed)

# css 이미지 크기 고정, div 가운데 맞춤



웹 페이지 화면을 구성하다보면 가장 짜증스러운 것이 css를 이용해 이미지 크기를 고정하는 것과 div를 가운데 맞춤 시키는 것이다. 

이것도 검색해보면 금방 나오지만 검색할 때마다 여러 사람들의 여러 답이 있고 그것이 제대로 적용되지 않는 경우가 많아서 그냥 내가 정리해보자는 마음으로 정리한다. 



<br>



# css 이미지 크기 고정



css 이미지 크기를 고정하는 것에 대한 아이디어는 이렇다 : 

img를 감싸는 div를 하나 만들고, 해당 div의 크기를 조정한다. img는 그래서 width: 100%, height: 100%로 만들어 div 크기만큼 되도록 고정한다.



<br> 

무슨 말인지는 코드를 통해 살펴보도록 하자. 



```html
        <div class ="GoodsImgWrapper">
            <img src="..." />
        </div>
```



<br>



위와 같은 코드가 있다고 하자. div(.GoodsImgWrapper) 가 img를 감싸고 있다. 

이 경우 div 의 스타일을 다음과 같이 지정하고, 



<br>



```css
        width: 60%; //원하는 크기 
        height: 60%;
        max-width: 60%;
        max-height: 60%;
        overflow: hidden;
```



<br>



Div 내의 img의 스타일은 다음과 같이 지정한다 .



<br>



```css
       height: 100%;
        width: 100%;
        max-height: 100%;
        max-width: 100%;
```



<br>



이렇게 해주면, 다음과 같이 이미지가 고정된 상태로 나온다. 



<br>



![imagae](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FKxUlO%2FbtqGuHtubNE%2F1hHKbhr6sKK9vuBfA53Wn0%2Fimg.png)



<br>



# div 가운데 맞춤



div 내에 div 를 가운데 맞춤시키는 건 쉽다. (div가 div로 감싸져 있지 않은 경우)



<br>



감싸고 있는 div에 `        text-align:center;` 속성을 주고, 

안에 있는 div에 `display: inline-block` 을 설정해주면 끝이다. 



<br>



여기에 `width: 85%;max-width: 85%;` 까지 붙이면 금상첨화 ! ggez 