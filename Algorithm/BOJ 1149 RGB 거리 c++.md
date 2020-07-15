# TIL 200715(Wed)

# BOJ 1149 RGB거리

<br>

```c++
#include <bits/stdc++.h>
using namespace std;

int s[1005][4];
int d[1005][4];

int main(void){
  ios::sync_with_stdio(0);
  cin.tie(0);
  int n;
  cin >> n;
  for(int i = 1; i <= n; i++) 
      cin >> s[i][1] >> s[i][2] >> s[i][3];
  d[1][1] = s[1][1]; // Red
  d[1][2] = s[1][2]; // Green
  d[1][3] = s[1][3]; // Blue
  for(int i = 2; i <= n; i++) {
    d[i][1] = min(d[i-1][2],d[i-1][3])+s[i][1];
    d[i][2] = min(d[i-1][1],d[i-1][3])+s[i][2];
    d[i][3] = min(d[i-1][1],d[i-1][2])+s[i][3];
  }
  cout << min(min(d[n][1],d[n][2]),d[n][3]); 
}
```

<br>

<br>