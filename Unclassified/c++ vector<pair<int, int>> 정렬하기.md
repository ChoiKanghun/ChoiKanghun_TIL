# TIL 200724(Fri)

# C++ pair<int, int> vector sort

## C++ pair vector 정렬하기



<br>



### 형식

vector<pair<int, int>> V ;

<br>



### 정렬

\< 을 쓰면 오름차순이고, \>를 쓰면 내림차순임. 

(사실 오름차순은 cmp함수를 아예 안 쓰면 됨. 오름차순이 디폴트이기 때문)

`first ` 를 기준으로 정렬하는 경우. First 가 같으면 second로 비교.

| 1234 | bool cmp(const pair<int, int> &a, const pair<int, int> &b){  return a.first < b.first;}[Colored by Color Scripter](http://colorscripter.com/info#e) | [cs](http://colorscripter.com/info#e) |
| ---- | ------------------------------------------------------------ | ------------------------------------- |
|      |                                                              |                                       |



<br>



`second` 를 기준으로 정렬하는 경우. second가 같으면 first로 비교 

  

| 1234 | bool cmp(const pair<int, int> &a, const pair<int, int> &b){  return a.second < b.second;}[Colored by Color Scripter](http://colorscripter.com/info#e) | [cs](http://colorscripter.com/info#e) |
| ---- | ------------------------------------------------------------ | ------------------------------------- |
|      |                                                              |                                       |



<br>