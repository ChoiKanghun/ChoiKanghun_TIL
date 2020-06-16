# TIL 200605(Fri)

## 스프링 파일 업로드 및 다운로드

웹 클라이언트가 서버에게 파일을 업로드할 때에는 HTTP 프로토콜의 바디 부분에 파일 정보를 담아서 전송을 하게 된다. 파일을 여러 개 보내면 다음과 같이 바디에 여러 개의 파일 정보가 담겨 온다.

<br>

 ![image-20200605214037477](C:\Users\User\AppData\Roaming\Typora\typora-user-images\image-20200605214037477.png)

  <br>

사진에서 볼 수 있듯이 Content-type, charset 등의 정보가 boundary(경계)로 나뉘어 들어오게 되고, 

이렇게 여러 부분으로 나눠서 오는 것을 MultiPart 데이터라고 한다.

 <br>

그런데 HttpServletRequest는 multipart 데이터를 알아서 나누어주지 않는다. 

HttpServletRequest는 HTTP 프로토콜의 바디를 읽어들이는 InputStream만을 지원한다. 

사용자는 이런 InputStream을 이용해서 MultiPart를 잘 나눠 사용해야 한다. 

 <br>

Spring MVC 파일을 업로드하려면 몇 가지 라이브러리와 설정을 추가해야 한다. 

MultiPart를 처리하기 위해서는 직접 구현하지 않고 주로 아파치에서 제공하는 `commons-fileupload` 라이브러리를 사용한다.  

또한 `commons-io`라이브러리를 추가되어야 하고, MultipartResolver Bean이 설정돼야 한다.

 <br>

라이브러리를 Maven으로 등록하는 것은 pom.xml에 해당 태그들을 추가하면 된다. 

 <br>

```xml
<dependency>
  <groupId>commons-fileupload</groupId>
  <artifactId>commons-fileupload</artifactId>
  <version>1.2.1</version>
</dependency>
<dependency>
  <groupId>commons-io</groupId>
  <artifactId>commons-io</artifactId>
  <version>1.4</version>
</dependency>
```

 <br>

DipsatcherServlet은 준비과정에서 multipart/form-data가 요청으로 들어올 경우에 
`MultipartResolver`를 사용하게 된다.  

이를 위해서는 MultipartResolver 객체를 생성하는 Bean을 설정해야 한다. 

설정 방식은 다음과 같다. 

 <br>

```java
@Bean
public MultipartResolver multipartResolver() {
	org.springframework.web.multipart.commons.CommonsMultipartResolver multipartResolver 
        = new org.springframework.web.multipart.commons.CommonsMultipartResolver();
	multipartResolver.setMaxUploadSize(10485760); // 1024 * 1024 * 10
	return multipartResolver;
}
```

 <br>

그리고 파일을 업로드할 때도 주의할 점이 있다. 

업로드 폼에서 enctype을 반드시 `multipart/form-data`로 설정해야 한다는 것이다.

(기본값은 `x-www-form-urlencoded`이다.) 

또한 input태그의 type이 `file`이어야 한다. 

 <br>

```html
<form method="post" action="/upload"
              enctype="multipart/form-data">
	......
	<input type="file" name="file">
	<input type="submit">
</form>
```

  

type이 file인 input 태그가 여러 개 있고 name 속성의 값이 같다면 file이 배열 형태로 컨트롤러에게 전달이 된다. 

 <br>

한편 컨트롤러에서는 어떤 설정이 필요할까?

 <br>

폼으로부터 전달되는 파일 정보를 Controller에서는 PostMapping으로 정보를 받는다. 

파일 정보는 파라미터로 전달되고, 이 때 MultipartFile type으로 전달된다. 

 <br>

파일을 여러 개 전달받을 경우 MultipartFile을 배열로 사용하도록 해주면 된다. 

MultipartFile의 메소드를 이용하면 업로드 되는 파일의 이름, 용량 inputStream을 구할 수 있다. 

 <br>

@RequestParam("file") MultipartFile file

@RequestParam("file") MultipartFile[] files

 <br><br>

 

#### 다운로드

 <br>

서버의 특정 디렉토리는 외부에서 접근할 수 없다. 

이런 파일을 외부에서 사용할 수 있도록 다운로드 기능을 제공해야 한다. 

파일을 다운로드하는 Controller메서드에서는 아래 코드와 같이 

먼저 헤더 정보에 사용자가 받으려는 파일 정보를 설정하고, 

캐시를 사용하지 않도록 설정해야 한다. 

그리고 나서 파일 정보를 HttpServlet의 Response의 OutpuStream으로 출력해야 한다.

 <br>

```markup
response.setHeader("Content-Disposition", "attachment; filename=\" + fileName + "\";);
response.setHeader("Content-Transfer-Encoding", "binary");
response.setHeader("Content-Type", contentType);
response.setHeader("Content-Length", fileLength;
response.setHeader("Pragma", "no-cache;");
response.setHeader("Expires", "-1;");
```

 <br>

refs - 

[**[FileUpload – Home\] **https://commons.apache.org](https://commons.apache.org/proper/commons-fileupload/)