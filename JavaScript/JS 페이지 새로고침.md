# TIL 200627(Sat)

# JavaScript 페이지 새로고침

### 페이지를 새로고침하는 3가지 방법

<br>

```
1. location.reload(true);

2. location.href = location.href;

3. history.go(0);
```

<br>

단순히 JavaScript 코드에 위 세 가지 코드 중 하나를 붙여넣는 것 만으로도 간단하게 새로고침이 가능하다.

두 번째의 `location.href`의 값으로 특정 url을 준다면 해당 페이지로 이동한다.

<br>



