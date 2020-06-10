# TIL 200609, 10(Tue, Wed)

# 알고리즘

# 퀵 정렬(Quick Sort)

## 개념

<br>

퀵 정렬은 아주 빠른 알고리즘으로, 가장 많이 사용된다. 

이 이름 또한 정렬 속도가 아주 빠르다는 뜻에서 지어졌다. 

퀵 정렬의 원리는 이렇다. 

어떤 나열된 자료형에서 가운데 값을 하나 선택한다. 

이 선택한 값을 `피벗(pivot)`으로 두고 피벗보다 큰 값을 가진 그룹과 작은 값을 가진 그룹으로 나눈다. 

해당 과정을 그룹 내 개수가 1개가 될 때까지 반복한다. 

<br><br>

## 개념도

<br>

![img](https://gmlwjd9405.github.io/images/algorithm-quick-sort/quick-sort.png)

출처 : https://gmlwjd9405.github.io/2018/05/10/algorithm-quick-sort.html

<br>

참고로 퀵 정렬도 문제를 잘개 쪼개어 해결한다는 점에서 분할정복법(divide-and-conquer)에 속한다.

<br><br>

## 배열을 두 그룹으로 나누기

<br>

배열을 통해 해당 개념을 소개한다. 

먼저 배열을 두 그룹으로 나누는 것부터 시작하자. 

<br>

먼저 다음과 같은 배열에서, 가운데 값인 6을 pivot으로 둔다. 

그리고 

arr[pl] >= pivot 

arr[pr] <= pivot 

이 성립되는 요소를 찾을 때까지 pl을 오른쪽으로, pr을 왼쪽으로 스캔한다. 

<br>

![image-20200610192143705](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fk.kakaocdn.net%2Fdn%2FncvJh%2FbtqEKQyt57R%2FTYqMT1GvRhDubxJVGHp8hk%2Fimg.png)

<br>

그리고 arr[pl]과 arr[pr]을 교환한다. 

그리고 이 과정을 pl이 pr보다 같거나 클 때까지 반복한다. 

반복한 결과는 다음과 같을 것이다. 

<br>

![image-20200610192118752](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fk.kakaocdn.net%2Fdn%2F20ofj%2FbtqEMjzsM9D%2FqZftfdgsVLwL3vUJnM3zl0%2Fimg.png)

<br>

pl과 pr이 교차하면 그룹을 나누는 과정이 끝나고 배열이 아래 두 그룹으로 나뉜다. 

<br>

피벗 이하의 그룹 : arr[0], ..., arr[pl - 1]

피벗 이상의 그룹 : arr[pr + 1], ..., arr[arr.length - 1]

<br>

개념과 원리를 살펴보며 어느 정도 감을 잡았다면, 이번에는 코드로 어떻게 작성하는지 살펴보자. 

<br>

<br>

## 코드로 구현하기

<br>

가장 먼저 두 그룹으로 나누는 것을 진행해보자. 

우리는 두 그룹으로 나누는 과정을 반복하면 될 뿐이다.

<br>

```java
	static void swap(int arr[], int index1, int index2) {
		int temp = arr[index1];
		arr[index1] = arr[index2];
		arr[index2] = temp;
	}

	static void quickSort(int arr[]) {
		int size = arr.length;
		int pl = 0;
		int pr = size - 1;
		int pivot = arr[(pl + pr) / 2];
		do {
			while (arr[pl] < pivot) pl++;
			while (arr[pr] > pivot) pr--;
			if (pl <= pr)
				swap(arr, pl++, pr--);
		} while (pl <= pr);
	}
```

<br>

위의 quickSort는 아직 정렬을 한 게 아니라 단순히 pivot을 기준으로 그룹을 나누었을 뿐이다. 

해당 그룹을 정렬될 때까지 나누는 코드는 다음과 같다. 

<br>

```java
public class QuickSort {

	static void swap(int arr[], int index1, int index2) {
		...
	}
	static void quickSort(int arr[], int farLeft, int farRight) {
		int pl = farLeft;
		int pr = farRight;
		int pivot = arr[(pl + pr) / 2];
		
		do {
			while (arr[pl] < pivot) 
				pl++;
			while (arr[pr] > pivot) 
				pr--;
			if (pl <= pr)
				swap(arr, pl++, pr--);
		} while (pl <= pr);
		System.out.println("\n현재 arr : ");
		for (int i = 0; i < arr.length; i++)
			System.out.print(arr[i] + " ");
		if (farLeft < pr)
			quickSort(arr, farLeft, pr);
		if (pl < farRight)
			quickSort(arr, pl, farRight);
	}
	
	public static void main(String[] args) {
		int arr[] = {1, 7, 2, 5, 3, 9, 8};
		System.out.println("sort 전 : ");
		for (int i = 0; i < arr.length; i++)
			System.out.print(arr[i] + " ");
		quickSort(arr, 0, arr.length - 1);
		System.out.println("\n결과 : ");
		for (int i = 0; i < arr.length; i++)
			System.out.print(arr[i] + " ");
	}
}

```

<br>

정렬이 일어날 때마다 해당 배열의 요소들의 상태를 출력하도록 설정했다. 

실제로 콘솔에 찍힌 결과는 다음과 같다. 

<br>

sort 전 : 

1  7  2  5  3  9  8  
현재 arr : 

1  3  2  5  7  9  8  
현재 arr : 

1  2  3  5  7  9  8  
현재 arr : 

1  2  3  5  7  9  8  
현재 arr : 

1  2  3  5  7  8  9  
현재 arr : 

1  2  3  5  7  8  9  
결과 : 

1  2  3  5  7  8  9  

<br>

## 퀵 정렬 (Quick Sort) import 하여 사용하기.

<br>

퀵 정렬이 빠르다고는 하지만, 매번 우리가 작성해 쓸 수는 없다. 

퀵 정렬을 따로 자바에서 제공할까? 

정답은 `yes`이다. 

<br>

java에서 제공하는 `Arrays.sort()`는 신기하게도 퀵 정렬을 이용한 정렬 메소드이다. 

다만 pivot을 두 개를 쓰는, 우리가 작성한 quick sort와는 조금 다르게 작동한다. 

이번 포스트에서 해당 정렬 로직을 다루지는 않겠다. 

어떻게 쓰는지, 그리고 잘 작동하는지 정도만 살펴보도록 하자.

<br>

먼저 `import java.util.Arrays;`을 import 해주고, 

main에서는 다음과 같이 사용한다. 

<br>

```java
public class QuickSort {
	public static void main(String[] args) {
		System.out.println("sort 전 : ");
		int arr2[] = {1, 7, 2, 5, 3, 9, 8};
		for (int i = 0; i < arr2.length; i++)
			System.out.print(arr2[i] + "  ");
        
		Arrays.sort(arr2);
		System.out.println("\n결과 : ");
		for (int i = 0; i < arr2.length; i++)
			System.out.print(arr2[i] + "  ");
	}
}
```

<br>

결과 :

<br>

sort 전 : 

1  7  2  5  3  9  8  
결과 : 

1  2  3  5  7  8  9  

<br>



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

