# boj 10250 ACM 호텔 c++

# 백준 10250 ACM 호텔 cpp



<br>



문제링크: https://www.acmicpc.net/problem/10250



<br>



시간적 여유가 있을 때에는 그것을 최대한 이점으로 삼고 넘어가자고 생각하게 만든 문제.

문제 자체는 쉬운데 괜히 초반에 n에서 h만큼씩 빼버리고 roomNumber를 구한 후 남은 n을 floorNumber에 더해줬다가 예외 케이스들 때문에 시간만 빼앗겼다.

n이 1씩 줄어들 때 floorNumber를 하나씩 증가시켜주고, 그것이 h보다 커지면 floorNumber를 1로 바꿔주고 roomNumber를 1 증가시킨다.

이 때 증가된 roomNumber가 w보다 크게 된다면 다시 roomNumber를 1로 바꿔주고 floorNumber를 1증가시킨다. 

최초로 floorNumber가 0인 이유는 h w n 각각이 1 1 1일 때를 생각해보면 알 수 있다.

아래는 정답코드이다.



<br>



```c++
#include <bits/stdc++.h>
using namespace std;

int main()
{
    ios::sync_with_stdio(0);
    cin.tie(0);
    
    int testcaseCount;
    cin >> testcaseCount;
    while (testcaseCount--)
    {
        int h, w, n;
        cin >> h >> w >> n;
        int roomNumber = 1;
        int floorNumber = 0;
        while (n--)
        {
            floorNumber++;
            if (floorNumber > h)
            {
                roomNumber++;
                floorNumber = 1;
            }
            if (roomNumber > w)
            {
                roomNumber = 1;
                floorNumber++;
            }
        }
        cout << floorNumber;
        if (roomNumber < 10)
            cout << 0;
        cout << roomNumber;
        if (testcaseCount)
            cout << "\n";
        // 바로 위의 if문 한 줄은 지워도 상관없다. 
        // 코딩테스트에서 공백 한 줄 다른 건 신경쓰지 않는다는 것을 배웠다.
    }
}
```



<br>

 

