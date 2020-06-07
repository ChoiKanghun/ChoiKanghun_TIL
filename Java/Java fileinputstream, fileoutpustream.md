# IL 200607(Sun)

# 자바 File.getInputStream, FileOutputStream

### File.getInputStream

 

다음과 같이 multipartFile file이 들어왔다는 가정 하에 설명하겠다.

 

```java
@PostMapping("/upload")
	public String upload(@RequestParam("file") MultipartFile file) {
```

 

이렇게 들어온 file은 `file.getOriginalFilename()`이나 `file.getSize()`와 같은 메서드를 지원한다. 

여러 가지 메서드 중에서 오늘 알아볼 것은 `getInputStream()`이다.  

사용형식은 다음과 같다.

 

```java
InputStream is = file.getInputStream();
```

 

이렇게 선언해주면 is에는 뭐가 담기게 될까? 바로 BLOB 객체다. 

BLOB 객체는 다음 사진과 같이 생긴 객체로, 주로 멀티미디어에 관한 객체다.

![https://heropy.blog/2019/02/28/blob/](https://heropy.blog/images/screenshot/blob/blob-file-object.jpg)

 

### FileOuputStream

읽어들인 blob 객체를 파일로 생성하고 싶을 때 사용하는 것이 FileOutputStream이다. 

 

```java
 FileOutputStream fos = new FileOutputStream(
                		"c:/tmp/" + file.getOriginalFilename() + new Date());
```

 

위와 같은 방식으로 생성하며, 괄호 안에 들어가는 매개변수는 생성할 파일의 경로 및 이름이다. 

new Date()를 붙여주는 이유는 중복 파일이 덮어쓰기 되는 것을 방지하기 위해서이다. 

 

### InputStream.read() & fileOutputStream.write

 

inputStream.read 메소드는 buffer를 인자로 받아 해당 buffer size 만큼 byte를 읽는다. 

그리고 FileOutputStream.write(buffer, offset, length) 는 

첫 번째 인자로 읽은 buffer를 offset부터 length만큼 출력한다. 

출력한다는 건 생성한다 내지 덧붙인다 정도로 해석하면 되겠다. 

사용예제에서 이것들이 어떻게 쓰이는 지 알아보자. 



### 사용예제 

 

```java
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
        } catch(Exception ex){
            throw new RuntimeException("file Save Error");
        }
		
		return "uploadok";
	}
}
```

 

결과 : 

```
파일 이름 : logback.gif
파일 크기 : 54733
0
1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
16
17
18
19
20
21
22
23
24
25
26
27
28
29
30
31
32
33
34
35
36
37
38
39
40
41
42
43
44
45
46
47
48
49
50
51
52
53
```







refs -

 

https://heropy.blog/2019/02/28/blob/ 

http://cris.joongbu.ac.kr/course/java/api/java/io/FileOutputStream.html 

http://blog.naver.com/PostView.nhn?blogId=eunjin6132&logNo=220888811967&parentCategoryNo=&categoryNo=55&viewDate=&isShowPopularPosts=true&from=search 

https://hyeonstorage.tistory.com/236 

https://comp.namoeditor.co.kr/cu/help/ko/dev/api/FileItem/Methods/getInputStream.html 

https://programmingsummaries.tistory.com/64 



