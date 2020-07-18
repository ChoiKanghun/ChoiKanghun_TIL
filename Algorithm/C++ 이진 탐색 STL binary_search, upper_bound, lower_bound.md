# TIL 200718(Sat)

# 알고리즘

# C++ 이진 탐색 STL binary_search, upper_bound, lower_bound

<br>
c++을 이용해 이진 탐색 문제를 풀어야 하는 경우, 직접 이진 탐색을 구현할 수도 있지만 워낙 오류도 많이 생기고 직접 구현하기가 느리기 때문에 STL을 많이 찾게 된다.
<br>
c++ 에서 이런 경우 어떤 STL을 제공하는지 알아보자.
<br>

## binary_search

<br>
가장 먼저 `binary_search`이다. 
binary_search는 인자로 배열의 시작주소, 시작주소 + 배열 크기, 그리고 val을 받는다. 
binary_search와 이후 설명할 upper_bound, lower_bound는 먼저 sort를 해주고 써야 한다.

<br>

`binary_search(arr, arr + n, val)`

<br> 

리턴 값은 1(true) 혹은 0(false) 이며, val이 arr ~ arr + n 사이에 있는 경우가 1, 없는 경우가 0이다.

<br><br>

### 예제

<br>

[백준 1920번](https://www.acmicpc.net/problem/1920) 문제는 STL binary_search를 딱 적용하기 좋은 문제다.

<br>

답안 코드
<br>

```c++
#include <bits/stdc++.h>
using namespace std;

int main () {
    ios::sync_with_stdio(0);
    cin.tie(0);

    int n, m;
    int arrN[100005];
    cin >> n;
    for (int i = 0; i < n; i++)
        cin >> arrN[i];
    cin >> m;
    //여기까지 입력.
    //STL 시작.
    sort(arrN, arrN + n);
    int t;
    for (int i = 0; i < m; i++) {
        cin >> t;
        cout << binary_search(arrN, arrN + n, t) << '\n';
    }
}
```

<br>

## upper_bound, lower_bound

<br>


그런데 만약 [백준 10816번](https://www.acmicpc.net/problem/10816) 과 같이 val와 일치하는 값이 몇 개나 있는지 알아보려면 어떻게 해야 할까? 이 경우 사용할 수 있는 STL이 바로 `upper_bound`와 `lower_bound`이다. 

<br>

`upper_bound (arr, arr + n, val)` 과 같은 형식으로 쓸 수 있다. 
리턴 값의 경우 `upper` 인지 `lower`인지에 따라 값이 조금 다른데, 
`upper_bound`의 경우 val이 담긴 마지막 요소의 다음 주소를 반환한다. 
그리고 `lower_bound`의 경우 val이 담긴 첫 번째 요소의 다음 주소를 반환한다.
<br>

예제 코드
(참고로 upper_bound, lower_bound는 아까 말했듯 sort를 해주고 써야 한다.)

<br>

```c++
#include <iostream>     // std::cout
#include <algorithm>    // std::lower_bound, std::upper_bound, std::sort

using namespace std;

int main () {
  int myints[] = {10,20,30,30,20,10,10,20};

  sort (myints, myints + 8);                // 10 10 10 20 20 20 30 30

  int *low, *up, *low2, *up2;
  low=lower_bound (myints, myints + 8, 77);
  up=upper_bound (myints, myints + 8, 77); 
  low2=lower_bound (myints, myints + 8, 20); 
  up2=upper_bound (myints, myints + 8, 20); 
  cout << "lower_bound at position " << (low) << '\n';
  cout << "upper_bound at position " << (up) << '\n';
  cout << "difference betweent up and low" << up - low << '\n';
  cout << "lower_bound at position " << (low2) << '\n';
  cout << "upper_bound at position " << (up2) << '\n';
  cout << "difference betweent up2 and low2" << up2 - low2 << '\n';

  return 0;
}
```

<br>

arr 대신 vector를 넣을 수도 있는데, 이에 대한 건 공식 문서를 참조하자. 
[Reference](http://www.cplusplus.com/reference/algorithm/upper_bound/) <- 이곳에서 upper_bound 및 lower_bound에 대한 공식 설명을 볼 수 있다. 