# TIL 200714(Tue)

# 알고리즘

# BOJ 9663 Nqueen c++

<br>

```c++
#include <bits/stdc++.h>
using namespace std;

int n;
int answer = 0;
int isusedCol[40]; // 열이 쓰였는지.
int isusedUpRight[40]; // 우상향 대각선이 쓰였는지.
int isusedDownRight[40]; // 우하향 대각선이 쓰였는지.

void nqueen(int cur) {
    if (cur == n) {
        answer++;
        return ;
    }
    for (int i = 0; i < n; i++) {
        //i는 인덱스이자 행값. cur은 열값.
        //x+y가 같으면 대각선상에 있는 좌표임. x-y도 마찬가지.
        //n-1을 isusedDownRight에 붙여주는 이유는 0 밑으로 가는 걸 방지하기 위해.
        if (isusedCol[i] || isusedUpRight[i + cur] || isusedDownRight[cur - i + n - 1])
            continue ;
        isusedCol[i] = 1;
        isusedUpRight[i + cur] = 1;
        isusedDownRight[cur - i + n - 1] = 1;
        nqueen(cur + 1);
        isusedCol[i] = 0;
        isusedUpRight[i + cur] = 0;
        isusedDownRight[cur - i + n - 1] = 0;
    }
}

int main() {
    ios::sync_with_stdio(0);
    cin.tie(0);
    
    cin >> n;
    fill(isusedCol, isusedCol + 40, 0);
    fill(isusedUpRight, isusedUpRight + 40, 0);
    fill(isusedDownRight, isusedDownRight + 40, 0);
    nqueen(0);
    cout << answer;
    return 0;
}
```

