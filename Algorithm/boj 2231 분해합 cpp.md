# BOJ 2231 cpp 분해합

# 백준 2231 c++ 분해합



<br>



처음에는 이게 난이도 하의 문제라는 것에 당황했다. 어떤 숫자의 조합이 목표가 되는 숫자로 표현되는지 안 되는지를 2초 안에 판단하라니. 그것도 최대 크기가 1000000인데!

하지만 이내 999999라는 가장 큰 숫자도 자신 + 54까지의 범위밖에 커버하지 못한다는 것을 깨닫고 2초면 차고 넘치는 시간이라는 것을 깨달았다.  



<br>



풀이 방법은 이렇다. 

예를 들어 198이라는 숫자가 있으면 해당 숫자의 분해합은 198 + 1 + 9 + 8인데, 여기서 1,9,8은 198이라는 숫자를

1. %10 해버린 값.
2. 10으로 한 번 나누고 %10 해버린 값
3. 10으로 두 번 나누고 %10 해버린 값

이므로 분해합을 구하고 싶은 숫자가 10보다 큰 동안 재귀를 사용하면 되는 것이다. 

해당 로직이 구현된 함수가 아래의 solve 함수이다. 



<br>



시간은 넉넉하다. 최대 54번만 구하면 되니까. for문의 i가 원하는 값을 찾지 못하면 0을 출력한다.

```c++
#include <bits/stdc++.h>
using namespace std;

int N;

int solve(int num)
{
    int res = 0;
    if (num >= 10)
        res += solve(num / 10);
    return res + (num % 10);
}

int main()
{
    ios::sync_with_stdio(0);
    cin.tie(0);
    
    cin >> N;
    if (N >= 54)
    {
        for (int i = N - 54; i < N; i++)
        {
            if (solve(i) + i == N)
            {
                cout << i;
                return 0;
            }
        }
    }
    else
    {
        for (int i = 1; i < N; i++)
        {
            if (solve(i) + i == N)
            {
                cout << i;
                return 0;
            }
        }
    }
    cout << "0";
    return 0;
}
```



<br>

