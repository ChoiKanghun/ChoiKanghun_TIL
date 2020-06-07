# TIL 200607(Sun)

## Spring 파일업로드, 다운로드 구현하기

 <br><br>

### 환경설정

Spring MVC에서 파일을 업로드하려면 몇 가지 라이브러리와 설정을 추가해야 한다. 

MultiPart를 처리하기 위해서는 직접 구현하지 않고 주로 아파치에서 제공하는 `commons-fileupload` 라이브러리를 사용한다.  

또한 `commons-io`라이브러리를 추가되어야 하고, MultipartResolver Bean이 설정돼야 한다.

 <br><br>

라이브러리를 Maven으로 등록하는 것은 pom.xml에 해당 태그들을 추가하면 된다. 

 <br><br>

```xml
<dependency>
  <groupId>commons-fileupload</groupId>
  <artifactId>commons-fileupload</artifactId>
  <version>1.2.1</version>
</dependency>
<!--위를 통해 API 추가.-->

<dependency>
  <groupId>commons-io</groupId>
  <artifactId>commons-io</artifactId>
  <version>1.4</version>
</dependency>
```

  <br><br>

DipsatcherServlet은 준비과정에서 multipart/form-data가 요청으로 들어올 경우에 
`MultipartResolver`를 사용하게 된다.  

이를 위해서는 MultipartResolver 객체를 생성하는 Bean을 설정해야 한다. 

설정 방식은 WebMvcConfigurerAdapter 를 상속받는 클래스에 다음을 추가해주는 것이다.

 <br><br>

```java
@Configuration
@EnableWebMvc
@ComponentScan(basePackages = {...})
public class WebMvcContextConfiguration extends WebMvcConfigurerAdapter {
...
	@Bean
	public MultipartResolver multipartResolver() {
	    org.springframework.web.multipart.commons.CommonsMultipartResolver multipartResolver 
            = new org.springframework.web.multipart.commons.CommonsMultipartResolver();
	    multipartResolver.setMaxUploadSize(10485760); // 1024 * 1024 * 10
	    return multipartResolver;
	}	
}
```

  <br><br>

위 코드에서 setMaxUploadSize를 통해 파일의 크기를 제한한다. 

1024 * 1024 * 10 은 10MB를 의미한다. 

 <br><br>

### 테스트해보기

 <br><br>

#### Controller

```java
@Controller
public class FileController {

    // get방식으로 요청이 올 경우 업로드 폼을 보여줍니다.
	@GetMapping("/uploadform")
	public String uploadform() {
		return "uploadform";
	}
	
	@PostMapping("/upload")
	public String upload(@RequestParam("file") MultipartFile file) {
		
		System.out.println("파일 이름 : " + file.getOriginalFilename());
		System.out.println("파일 크기 : " + file.getSize());
		
        try(
                /* 맥일 경우 
                FileOutputStream fos = new FileOutputStream(
        			"/tmp/" + file.getOriginalFilename() + new Date());
        		*/
        		
                // 윈도우일 경우
                FileOutputStream fos = new FileOutputStream(
                		"c:/tmp/" + file.getOriginalFilename() + new Date());
                InputStream is = file.getInputStream();
        ){
        	    int readCount = 0;
        	    byte[] buffer = new byte[1024];
        	    int i = 0;
            while((readCount = is.read(buffer)) != -1){
                fos.write(buffer, 0, readCount);
                System.out.println(i++);
            }
        }catch(Exception ex){
            throw new RuntimeException("file Save Error");
        }
		
		
		return "uploadok";
	}
}
```

 <br>

* 여기서 stream들에 대해 궁금한 점이 있다면 다음 포스트 확인 :
  https://42kchoi.tistory.com/manage/posts/

  <br><br>

#### JSP

1. uploadform.jsp

   ```java
   <%@ page language="java" contentType="text/html; charset=UTF-8"
       pageEncoding="UTF-8"%>
   <!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
   <html>
   <head>
   <meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
   <title>uploadform</title>
   </head>
   <body>
   <h1>Upload Form</h1>
   <br><br>
    <form method="post" action="upload" enctype="multipart/form-data">
   
       file :    <input type="file" name="file"><br>
   
           <input type="submit">
    </form>    
   </body>
   </html>   
   ```

   <br><br>

2. uploadok.jsp

   ```java
   <%@ page language="java" contentType="text/html; charset=UTF-8"
       pageEncoding="UTF-8"%>
   <!DOCTYPE html>
   <html>
   <head>
   <meta charset="UTF-8">
   <title>Insert title here</title>
   </head>
   <body>
   	<div>Upload OK</div>
   </body>
   </html>
   ```

<br><br>

### 테스트 결과

![fileuploadtest](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fk.kakaocdn.net%2Fdn%2FcMmlmb%2FbtqEGCsW1Is%2F1YPDW6pvEWBBWHnHSAkMGK%2Fimg.gif)

### 다운로드 구현하기

<br>

먼저 파일을 다운로드 하는 주소를 "/download"로 놓고, 컨트롤러를 작성한다. 

<br><br>

```java
	@GetMapping("/download")
	public void download(HttpServletResponse response) {

        // 직접 파일 정보를 변수에 저장해 놨지만, 이 부분이 db에서 읽어왔다고 가정한다.
		String fileName = "connect.png";
		String saveFileName = "c:/tmp/connect.png"; 
        // 맥일 경우 "/tmp/connect.png" 로 수정
		String contentType = "image/png";
		int fileLength = 116303;
		
        response.setHeader("Content-Disposition", "attachment; filename=\"" + fileName + "\";");
        response.setHeader("Content-Transfer-Encoding", "binary");
        response.setHeader("Content-Type", contentType);
        response.setHeader("Content-Length", "" + fileLength);
        response.setHeader("Pragma", "no-cache;");
        response.setHeader("Expires", "-1;");
        
        try(
                FileInputStream fis = new FileInputStream(saveFileName);
                OutputStream out = response.getOutputStream();
        ){
        	    int readCount = 0;
        	    byte[] buffer = new byte[1024];
            while((readCount = fis.read(buffer)) != -1){
            		out.write(buffer,0,readCount);
            }
        }catch(Exception ex){
            throw new RuntimeException("file Save Error");
        }
	}
```

<br><br>

### 테스트 결과

![img](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fk.kakaocdn.net%2Fdn%2F3EiWu%2FbtqEGfLzIro%2FPVtJmL9Py95ARhZ9Z6Ku31%2Fimg.gif)

