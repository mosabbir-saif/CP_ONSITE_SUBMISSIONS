# C. Self Citation

**Time limit per test:** 3 s  
**Memory limit per test:** 256 MB

## Problem Statement

Professor Aubergine cares a lot about his citation count. He wants to increase his total number of citations as much as possible.

He plans to publish exactly $n$ papers over the next $k$ months. In the $i$-th month, he can publish at most $a_i$ papers due to submission limits.

Every paper he publishes in a month self-cites all of his papers published in all previous months. However, papers published in the same month cannot cite each other.

Let $b_i$ be the number of papers he publishes in month $i$. Your task is to find a sequence $b_1, b_2, \dots, b_k$ that gives the maximum possible number of total citations. The sequence must satisfy $0 \le b_i \le a_i$ for all $i$, and the total sum of all $b_i$ must be exactly $n$.

## Input

The first line contains a single integer $t$ ($1 \le t \le 10^3$) — the number of test cases. Then the description of the test cases follows.

The first line of each test case contains two space-separated integers $n$ and $k$ ($1 \le n \le 2 \cdot 10^{15}$, $1 \le k \le 2 \cdot 10^6$) — the total number of papers and the number of months.

The second line of each test case contains $k$ space-separated integers $a_1, a_2, \dots, a_k$ ($0 \le a_i \le 10^9$, $n \le a_1 + a_2 + \dots + a_k$) — the maximum number of papers he can publish in each month.

It is guaranteed that the sum of $k$ over all test cases does not exceed $2 \cdot 10^6$.

## Output

For each test case, print $k$ space-separated integers $b_1, b_2, \dots, b_k$ — the optimal number of papers to publish each month.

If there are multiple sequences that give the same maximum number of citations, you may print any of them.

## Examples

**Input**
2
10 3
3 4 5
12 3
2 4 10

**Output**
3 3 4 
2 4 6 


## Solve(C++)

```cpp
#include <bits/stdc++.h>
#define int long long
using namespace std;

void solve() {
    
    int n, m;
    cin >> m >> n;
    set<int>st;
    vector<int>v(n), tar(n, 0);
    for(int i = 0; i < n; i++){
        cin >> v[i];
        st.insert(i);
    }
    while(m > 0){
        if(st.empty()) break;
        int avg = max(1LL, m / (int)st.size());
        set<int>temp = st;
        for(auto x : st){
            int dig = min(avg, min(v[x], m));
            tar[x] += dig;
            v[x] -= dig;
            m -= dig;
            if(v[x] == 0){
                temp.erase(x);
            }
        }
        st = temp;
    }
    for(auto x : tar) cout << x << " ";
    cout << endl;
}

signed main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);
    
    int t;
    cin >> t;
    while (t--) {
        solve();
    }
}
```
