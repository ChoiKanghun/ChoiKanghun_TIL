# TIL 200706(Mon)

# 알고리즘

# BOJ 10866

## 덱 cpp



```c++
#include <bits/stdc++.h>
using namespace std;
/*
    push_front X: 정수 X를 덱의 앞에 넣는다.
	push_back X: 정수 X를 덱의 뒤에 넣는다.
	pop_front: 덱의 가장 앞에 있는 수를 빼고, 그 수를 출력한다. 
		만약, 덱에 들어있는 정수가 없는 경우에는 -1을 출력한다.
	pop_back: 덱의 가장 뒤에 있는 수를 빼고, 그 수를 출력한다. 
		만약, 덱에 들어있는 정수가 없는 경우에는 -1을 출력한다.
	size: 덱에 들어있는 정수의 개수를 출력한다.
	empty: 덱이 비어있으면 1을, 아니면 0을 출력한다.
	front: 덱의 가장 앞에 있는 정수를 출력한다. 만약 덱에 들어있는 정수가 없는 경우에는 -1을 출력한다.
	back: 덱의 가장 뒤에 있는 정수를 출력한다. 만약 덱에 들어있는 정수가 없는 경우에는 -1을 출력한다.
*/
int main() {

    ios::sync_with_stdio(0);
    cin.tie(0);
    deque<int> dq;
    string s;
    int n;
    int input;
    
    cin >> n;
    while (n--) {
        cin >> s;
        if (s == "push_front") {
            cin >> input;
            dq.push_front(input);
        } else if (s == "push_back") {
            cin >> input;
            dq.push_back(input);
        } else if (s == "pop_front") {
            if (dq.empty()) {
                cout << -1 << '\n';
            } else { //dq이 비어있지 않으면
                cout << dq.front() << '\n';;
                dq.pop_front();
            }
        } else if (s == "pop_back") {
            if (dq.empty()) {
                cout << -1 << '\n';
            } else {
                cout << dq.back() << '\n';
                dq.pop_back();
            }
        } else if (s == "size") {
            cout << dq.size() << '\n';
        } else if (s == "empty") {
            cout << dq.empty() << '\n';
        } else if (s == "front") {
            if (dq.empty()) {
                cout << -1 << '\n';
            } else {
                cout << dq.front() << '\n';        
            }
        } else { //s==back
            if (dq.empty()) {
                cout << -1 << '\n';
            } else {
                cout << dq.back() << '\n';        
            }
        }
    }
}
```

