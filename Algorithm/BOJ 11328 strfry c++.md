# BOJ 11328 strfry c++

# 백준 11328 strfrya c++



<br>



```c++
#include <bits/stdc++.h>
using namespace std;

int testCaseCount;
string tempLine;

void solve(string tempLine, int arr[]) {
    for (char c: tempLine) 
        arr[c] -= 1;
    
    int len = tempLine.size();
    for (int i = 0; i < 150; i++) {
        if (arr[i] != 0) {
            cout << "Impossible" << '\n';
            return ;
        }
    }
    cout << "Possible" << '\n';
}

int main() {
    ios::sync_with_stdio(0);
    cin.tie(0);
    
    cin >> testCaseCount;
    while (testCaseCount--) {
        int arr[150] = {};
        cin >> tempLine;
        for (char c: tempLine) {
            arr[c]++;
        }
        cin >> tempLine;
        solve(tempLine, arr);
    }
}
```



<br>

