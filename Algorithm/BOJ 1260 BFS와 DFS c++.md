# TIL 200722(Wed)

## BOJ 1260 BFS와 DFS c++

## 백준 1260 BFS와 DFS c++

<br>

```c++
#include <bits/stdc++.h>
using namespace std;

int v, e, start;
vector<int> adj[1005];
bool vis[1005];

void dfs(int cur) { //cur은 방문한 adj[]의 index
    cout << cur << ' ';
    for (int i = 0; i < adj[cur].size(); i++) {
        int nxt = adj[cur][i];
        if (vis[nxt])
            continue;
        vis[nxt] = true;
        dfs(nxt);
    }
}

void bfs() {
    queue<int> Q;
    Q.push(start);
    vis[start] = true;
    while (!Q.empty()) {
        int cur = Q.front();
        Q.pop();
        cout << cur << ' ';
        for (int i = 0; i < adj[cur].size(); i++) {
            int nxt = adj[cur][i];
            if (vis[nxt])
                continue;
            Q.push(nxt);
            vis[nxt] = true;
        }
    }
}

int main() {
    ios::sync_with_stdio(0);
    cin.tie(0);
    
    int a, b;
    cin >> v >> e >> start;
    while (e--) {
        cin >> a >> b;
        adj[a].push_back(b);
        adj[b].push_back(a);
    }
    for (int i = 1; i <= v; i++)
        sort(adj[i].begin(), adj[i].end());
    vis[start] = true;
    dfs(start);
    cout << '\n';
    fill(vis, vis + v + 1, false);
    bfs();
}
```

<br>

분류 : 그래프 - BFS, DFS

<br>



