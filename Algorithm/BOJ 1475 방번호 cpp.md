# BOJ 1475 방 번호 c++

# 백준 1475 방 번호 c++



<br>



```c++
#include <bits/stdc++.h>
using namespace std;

int n;
string line;
int arr[256];

int main() {
    ios::sync_with_stdio(0);
    cin.tie(0);
    
    cin >> n;
    line = to_string(n);
    for (char c: line)
        arr[(int)c]++;
    char c = '6';
    int six = arr[(int)c];
    arr[(int)c] = 0;
    arr[(int)c+3] += six;
    bool isOdd = arr[(int)c + 3] % 2 == 1 ? true : false;
    arr[(int)c+3] = (arr[(int)c+3]) / 2;
    if (isOdd)
        arr[(int)c+3]++;
    int ans = *max_element(arr, arr+256);    
    cout << ans;
    
}
```



<br>



* max_element(시작주소, 끝 주소+1) 은 시작주소부터 끝 주소까지 중에서 가장 큰 요소의 주소를 반환함.





<br>





