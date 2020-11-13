### Handlebars if 그리고 unless + handlebars 인덱스(첫 번째, 마지막 인덱스)

(#handlebars 부정문자, #handlebars 부정문, #handlebars 부정연산자, #handlebars !)

```html
//1. if
{{#if @first}}
  <td>첫번째 상품 ({{@key}} 번째 요소)</td>
{{else if @last}}
  <td>마지막 상품 ({{@key}} 번째 요소)</td>
{{else}}
  <td>중간 아이템 ({{@key}} 번째 요소)</td>
{{/if}}

//2. unless
{{#each productPrices}}
      {{price}}원
  {{#unless @last}}
    /
  {{/unless}}
{{/each}}

```

1. 



refs

https://sailboat-d.tistory.com/30 - handlebars 이용시 첫 번째 객체에만 접근하기