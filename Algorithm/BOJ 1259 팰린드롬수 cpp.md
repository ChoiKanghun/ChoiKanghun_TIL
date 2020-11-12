# BOJ 1259 팰린드롬수 c++

# 백준 1259 팰린드롬수 cpp



<br>



자꾸 string에 strlen 함수를 적용시키게 된다 ...

문자열의 길이를 반환하는 함수로서 string 형태의 글자 개수를 반환하는 것은 .length() 임을 기억하자. 



<br>



해당 문제는 i라는 인덱스가 0 -> len-1 까지 갈 때 j라는 인덱스는 그 반대로서 len - 1 부터 0으로 움직이게 한 뒤에 그들 인덱스에 해당하는 문자들이 똑같은지 확인하는 문제다. 난이도는 매우 쉬움 정도.



<br>





문제링크 : https://www.acmicpc.net/problem/1259



<br>



```c++
#include <bits/stdc++.h>
using namespace std;

int main()
{
    ios::sync_with_stdio(0);
    cin.tie(0);
    
    string str;
    while (true)
    {
        bool isno = false;
        cin >> str;
        if (str == "0")
            return 0;
        int len = str.length();
        for (int i = 0; i < len; i++)
        {
            int j = len - 1 - i;
            if (str[i] != str[j])
            {
                isno = true;
                break;
            }
        }
        if (isno)
            cout << "no\n";
        else
            cout << "yes\n";       
    }
}
```

