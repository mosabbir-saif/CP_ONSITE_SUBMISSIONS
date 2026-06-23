# A. Edgy Graph
##### time limit per test: 1 second  
##### memory limit per test: 256 megabytes

You are given an undirected graph with n vertices and m edges, where each edge has a positive weight. Construct an array a of size n such that:

- 1 ≤ ai ≤ 10^9 for all 1 ≤ i ≤ n.
- For every edge (u, v) with weight w, max(au, av) = w.

**Input**
- t (1 ≤ t ≤ 1e5) — number of test cases.
- For each test case:
    - n and m (2 ≤ n ≤ 3·10^5, 1 ≤ m ≤ 3·10^5).
    - m lines follow: u, v, w (1 ≤ u, v ≤ n, 1 ≤ w ≤ 10^9). No self-loops or multiple edges.
- Sum of n and sum of m across all test cases ≤ 3·10^5.

**Output**
For each test case output n integers a1, a2, …, an — any valid array satisfying the conditions, or -1 if impossible.

**Example**

**INPUT**
```
3
3 3
1 2 1
2 3 2
3 1 2
3 3
1 2 1
2 3 2
1 3 3
3 1
1 2 5
```

**OUTPUT**
```
1 1 2
-1
1 5 1000000000
```

### Solution (C++)

```cpp
#include <bits/stdc++.h>
#define ll long long
using namespace std;
const int INF = 1e9;

void solve(){

    int x, y;
    cin >> x >> y;
    vector<tuple<int, int, int>>v;
    vector<int>dist(x + 1, INF);
    for(int i = 0; i < y; ++i){
        int a, b, c;
        cin >> a >> b >> c;
        v.emplace_back(a, b, c);
        dist[a] = min(dist[a], c);
        dist[b] = min(dist[b], c);
    }
    bool flag = true;
    for(auto &[a, b, c] : v){
        if(max(dist[a], dist[b]) != c){
            flag = false;
            break;

        }
    }
    if(!flag){
        cout << -1 << endl;
        return;
    }
    for(int i = 1; i <= x; ++i){
        cout << dist[i] << " ";
    }
    cout << endl;
}

int main() {
    
    ios::sync_with_stdio(false);
    cin.tie(nullptr);
    cout.tie(nullptr);
    
    int t;
    cin >> t;
    while(t--){
        solve();
    }
}
```
