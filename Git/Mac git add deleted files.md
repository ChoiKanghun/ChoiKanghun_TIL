# TIL 200629(Mon)

# Mac git deleted files add(삭제 파일 add하기)

 맥에서

git add *

명령어를 통해 모든 파일을 add시켜도 아래와 같이 삭제한 파일은 staging 되지 않는다.

 

![img](https://k.kakaocdn.net/dn/ntgJ5/btqFeNtJB8q/Chtpk1buQObt7QtLN0BTn1/img.png)

 

이 경우 삭제한 파일까지 staging 시키기 위해서는 -A라는 옵션을 붙여준다.

 

git add -A : stages All (include new files, modified and deleted)

 

해당 옵션을 붙여주면 아래 사진과 같이 삭제된 파일도 잘 add된 것을 확인할 수 있다.

 



![img](https://k.kakaocdn.net/dn/c96spn/btqFcOt2QwB/iJo15zjGvK62iufowyKx1K/img.png)



 

 

참고로 아래와 같은 명령어를 통해 삭제한 것은 스테이지하지 않도록 할 수도 있다.

 

git add . :stages new and modified, without deleted

git add -u : stages modified and deleted, without new

 