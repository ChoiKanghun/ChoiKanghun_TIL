# 42 API 사용법

<br>

먼저 42에 로그인한다.

그런 다음, 좌측 sidebar의 나침반을 클릭한다.

나침반을 클릭했을 때 나오는 4가지 메뉴 중 API를 클릭한다. 

<br>



![img](https://k.kakaocdn.net/dn/ccgYiP/btqESGXzxUP/tQR8lSVmyOm4MoC0kl64k1/img.png)

<br>

그러면 다음과 같은 화면이 나온다.

<br>

![img](https://k.kakaocdn.net/dn/IVqDE/btqETnpKUOv/24O5lfYmZacPm4hCOIvhi0/img.png)

<br>

GET started를 클릭한다. 

그러면 다음 사이트가 나온다. 

<br>

![img](https://k.kakaocdn.net/dn/O6FQ5/btqETLKnCwj/XEjlywfgLEPoD1CeENuWCk/img.png)



<br>

위 사이트에서 하늘색 **here**을 클릭한다. 

그러면 다음 사진과 같은 화면이 뜰 것이다.

<br>

![img](https://k.kakaocdn.net/dn/buVkIJ/btqEUps8nJ1/lCUwcEBTDiczhLPFLdVEqK/img.png)

<br>

모든 요구사항을 적어넣고 제출한다.

<br>

![img](https://k.kakaocdn.net/dn/r26de/btqETYW7C16/N5QjZuHvEtbbKDXpckVp71/img.png)

<br>

화면 우상단의 아이디에 마우스를 갖다 대면 위와 같은 그림이 뜬다.

Settings를 누른다.

<br>



![img](https://k.kakaocdn.net/dn/0BYsQ/btqETBH1dGI/masM2hkzeAuMvQInEu5cOk/img.png)



settings를 누르면 나오는 사이드바의 API를 누른다. 

<br>

누르면 제일 위에 내가 등록한 API가 나온다. 

<br>

![img](https://k.kakaocdn.net/dn/Jg5Zk/btqEVIZ2A96/3LaQzxvEzqump2EwfvfIhk/img.png)

<br>

내가 만든 API(위 그림의 42SEOUL YOUTUBE STUDIO)를 클릭해보자.

<br>

클릭하면 아래와 같은 정보들이 노출된다. 

<br>



![img](https://k.kakaocdn.net/dn/bslSzJ/btqETmRXY21/xNo86800HVErDFyArDfBK0/img.png)

![img](https://k.kakaocdn.net/dn/ctaOi7/btqETKxXWkF/8HfTq9mhJZwnstvqWHiMIk/img.png)

<br>

여기서 redirect URI 밑의 빨간색 글자 밑에 있는 글자를 복사해 붙여 넣으면, 우리가 설정한 URI로 리다이렉트 되는데, 이 때 리다이렉트 주소 뒤에 code=a123asd1f12412dzv... 와 같은 정보가 딸려 온다. 

이 code는 꼭 필요하다. 

이것을 필자는 Spring으로 @RequestParam(name="code")String code 이렇게 받았는데, 

여러분은 각자 사용하는 서버로 꼭 받아서 code를 사용할 수 있게 만들자.  

(참고로 code를 못 받겠는 경우 제한적인 API 사용은 가능하다.  

아래 글에서 grant_type을 client_credentials 으로 설정하고 code 요청을 빼주면 된다.) 



<br>

아래는 code를 가져왔다고 가정하고 전개한다. 

<br>



이제 아래 조건대로 url 뒤에 query들을 붙여 요청해보자. 

url 뒤의 쿼리란 예를 들면 아래의 name, age와 같다. 

<br>

```
https://api.intra.42.fr/oauth/token?name=kchoi&age=26
```

<br><br>

## 조건

<br>

query : 

(아까 API 페이지에서 보았던 정보들이 요구된다. 더불어 code도.)

```
queryString += "" 
	+ "grant_type=" + "authorization_code" + "&"
	+ "client_id=" + 아까 API 페이지에서의 UID + "&" 
	+ "client_secret=" + 아까 API 페이지에서의 Secret + "&" 
	+ "code=" + inputCode.value + "&"
	+ "redirect_uri=" + 아까 API 페이지에서의 Redirect URI + "&"
	+ "scope=public";
```

<br>

요청 url 및 request 방식:

(oReq는 내가 설정한 XMLHttpRequest 변수이다.)

<br>

```
oReq.open('POST', "https://api.intra.42.fr/oauth/token");
```

<br>

request시 요청 헤더

<br>

```
oReq.setRequestHeader('Content-Type', 'application/x-www-form-urlencoded');
oReq.setRequestHeader("X-Mobile", "false");
oReq.responseType = "text";
```



<br>

요청을 console.log로 찍어보면, 아래와 같은 결과가 나온다. 

<br>

![img](https://k.kakaocdn.net/dn/VoSfB/btqESXdKa1o/xKXQCSyrYJHi9KjkrhZs50/img.png)



<br>

우리는 이제 받아온 json에서 access_token을 뽑아낼 수 있다.(JSON.parse(this.responseText).access_token)

<br>

이 access_token이 있으면 이제 대부분의 API를 사용할 수 있게 된다. 

예를 들어 /v2/me 라는 API를 얻고 싶다면 아래와 같이 요청하여 정보를 얻어낸다.

<br>

```
var url = "https://api.intra.42.fr/v2/me";
var oReq = new XMLHttpRequest;

oReq.open('GET', url);
oReq.setRequestHeader("Authorization", "Bearer " + token);
oReq.setRequestHeader('Content-Type', 'application/json; charset=utf-8');
oReq.responseType = "text";
oReq.addEventListener('load', function() {
	console.log(JSON.parse(this.responseText));
});
oReq.send(); 
```

<br>

여기서 중요한 건 Authorization Header를 "Bearer " + token 으로 설정해야 한다는 것이다. 

(token은 내가 받아 온 access_token을 의미한다. Bearer 뒤에는 스페이스 하나가 들어가있다.)

<br>

받아온 API 정보는 다음과 같다. 

<br>

![img](https://k.kakaocdn.net/dn/dGaUnM/btqETXKEYxi/pk10ONhtW3PzKCkAQxLs10/img.png)





<br>

마지막으로 리팩토링 1도 안한 raw code가 필요한 분들을 위해 code를 남겨놓겠다. 

<br>

```
<%@ page language="java" contentType="text/html; charset=UTF-8"
	pageEncoding="UTF-8"%>
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
</head>
<body>
	<%
		String code = (String) request.getAttribute("code");
		request.setAttribute("code", code);
	%>
	<form method='POST' action="https://api.intra.42.fr/oauth/token" 
		encType="application/json">
		<input name="grant_type" placeholder="grant_type"
			value="client_credentials"> <input name="client_id"
			placeholder="client_id"
			value="27ef6c6257d555818826985f9a1f85c85bf81ffe9d61780d4d6278cf845cddba">
		<input name="client_secret" placeholder="client_secret"
			value="068abc288188c153dd4eb402d7e2556e4d2bf804515584e81a5efa8c151b90f2">
		<input name="code" placeholder="code" value="${requestScope.code}">
		<input name="redirect_uri" placeholder="redirect_uri"
			value="http://localhost:8080/ftYoutube/getTokenPage">
		<button type="submit">button</button>
	</form>

	<form name="form2" method='GET' action="https://api.intra.42.fr/v2/me">
		<input type="text" name="inp" value="hi"></input>
		<button type="submit">form2</button>
	</form>

</body>
<script>
function AjaxClass() {	
}
AjaxClass.prototype.getApiWithToken = function(token) {
	var url = "https://api.intra.42.fr/v2/me";
	var oReq = new XMLHttpRequest;
	
	oReq.open('GET', url);
 	oReq.setRequestHeader("Authorization", "Bearer " + token);
	oReq.setRequestHeader('Content-Type', 'application/json; charset=utf-8');
	oReq.responseType = "text";
	console.log(token);
	oReq.addEventListener('load', function() {
		console.log(JSON.parse(this.responseText));
	});
	oReq.send(); 

}
	document.addEventListener("DOMContentLoaded", function() {

		var inputGrantType = document.querySelector("input[name=grant_type]");
		var inputClientId = document.querySelector("input[name=client_id]");
		var inputClientSecret = document
				.querySelector("input[name=client_secret]");
		var inputCode = document.querySelector("input[name=code]");
		var inputRedirectURI = document
				.querySelector("input[name=redirect_uri]");

		var oReq = new XMLHttpRequest;
		var queryString = "";
		queryString += "" 
				+ "grant_type=" + "authorization_code" + "&"
				+ "client_id=" + inputClientId.value + "&" 
				+ "client_secret=" + inputClientSecret.value + "&" 
				+ "code=" + inputCode.value + "&"
				+ "redirect_uri=" + inputRedirectURI.value + "&"
				+ "scope=public";
		oReq.open('POST', "https://api.intra.42.fr/oauth/token");
		oReq.setRequestHeader('Content-Type', 'application/x-www-form-urlencoded');
		oReq.setRequestHeader("X-Mobile", "false");
		oReq.responseType = "text";
		oReq.addEventListener('load', function() {
			var json = JSON.parse(this.responseText);
			var tokenFromAPI = json.access_token;
			var getApiAjaxObj = new AjaxClass();
			getApiAjaxObj.getApiWithToken(tokenFromAPI);
			console.log(json);
		});
		oReq.send(queryString); 
	})
	
	
</script>

</html>
```