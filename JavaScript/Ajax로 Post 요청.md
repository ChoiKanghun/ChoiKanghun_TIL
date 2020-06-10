# TIL 200610(Wed)

# 자바스크립트 AJAX POST (Vanilla Script)

<br>

oAuth를 쓰면서 비동기적으로 AJAX POST 요청을 하고, 그 요청에 대한 결과를 받아야 할 일이 있었다. 

처음에는 'GET이랑 똑같이 쓰면 되겠지..' 하고 방심했다가 큰코다쳤다. 

이번 포스트에서는 AJAX로 POST 요청하는 법에 대해 설명한다. 

<br>

먼저 oAuth 에서는 다음의 5가지를 POST 방식으로 보낼 것을 요구했다. 

5가지를 보내면 내가 원하는 token을 준다. 

<br>

* grant_type
* client_id
* client_secret
* code
* redirect_uri

<br>

해당필드들에 넣어야 할 value들을 input 태그의 value에 미리 넣어줬다.

form 형식으로 만들었지만, 실제로 submit 버튼을 통해 제출하지 않고 AJAX로 내용을 요청할 것이다. 

<br>

```jsp
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
```

<br>

위와 같이 input 요소들을 적어줬다면, 이번에는 javascript로 ajax 신청을 할 차례다. 

안정성을 위해 DOMContentLoaded 이후에 함수가 실행될 수 있도록 하였다. 

<br>

```javascript
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
				+ "grant_type=" + inputGrantType.value + "&"
				+ "client_id=" + inputClientId.value + "&" 
				+ "client_secret=" + inputClientSecret.value + "&" 
				+ "code=" + inputCode.value + "&"
				+ "redirect_uri=" + inputRedirectURI.value;
		oReq.open('POST', "https://api.intra.42.fr/oauth/token");
		oReq.setRequestHeader('Content-Type', 'application/x-www-form-urlencoded');
		oReq.responseType = "text";
		oReq.addEventListener('load', function() {
			var test = JSON.parse(this.responseText);
		});
		oReq.send(queryString); 

```

<br>

위를 잘 살펴보면, POST로 보낼 정보들을  

\1. 미리 가져오고, 

\2. 가져온 정보들을 하나씩 queryString 변수에 담아서, 

\3. (중요!) `Content-type` 헤더를 `application/x-www-form-urlencoded` 로 설정한다. 

\4. 마지막으로 queryString 변수를 send 해주면 

\5. oReq.addEventListener 함수 안에 들어 있는 test에 response(json)가 담기게 된다. 

<br><br>

## 결과 확인

<br>

실제로 아래와 같은 정보가 test 변수에 담긴다.

<br>

```json
{
"access_token": "3ef70cc28f5c64a14307b3d35ea09d071332ffe0a683621169342313471092c5",
"token_type": "bearer",
"expires_in": 7200,
"scope": "public",
"created_at": 1591781799
}
```

<br>

(이제 access_token을 서버에 다시 보내면 api를 사용할 수 있다.)

