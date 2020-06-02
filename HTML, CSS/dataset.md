### JavaScript

#### DataSet

 HTML, CSS, JS 에서는 dataset을 이용하여 좀더 효율적인 코딩을 할 수 있다.

##### HTML

 

어느 속성이든 dataset을 사용할 수 있다. 해당 속성으로 추가 정보를 속성에 담아 놓는 것이 목적이다.

 

##### `data` 사용법

 

```html
<article
  id="electriccars"
  data-columns="3"
  data-index-number="12314"
  data-parent="cars">
...
</article>
```

 

##### JavaScript 에서 사용하기

 

##### 문법

 

대상.dataset.data

  

##### 예제

 

```js
var article = document.getElementById('electriccars');
 
article.dataset.columns // "3"
article.dataset.indexNumber // "12314"
article.dataset.parent // "cars"
```

각 속성은 문자열이다. 값 변경도 가능하다. (ex - article.dataset.columns = 5) 

>  주의 ! : 대시들은 camelCase로 변환되는 것에 주의 ! (index-number => indexNumber)

 

##### CSS 에서 접근하기

데이터 속성은 CSS에서도 접근할 수 있다.  

 

##### 예제

 

```css
article::before {
  content: attr(data-parent);
}
```

 

```css
article[data-columns='3'] {
  width: 400px;
}
article[data-columns='4'] {
  width: 600px;
}
```

 

refs-



##### dataset

[https://developer.mozilla.org/ko/docs/Learn/HTML/Howto/%EB%8D%B0%EC%9D%B4%ED%84%B0_%EC%86%8D%EC%84%B1_%EC%82%AC%EC%9A%A9%ED%95%98%EA%B8%B0](