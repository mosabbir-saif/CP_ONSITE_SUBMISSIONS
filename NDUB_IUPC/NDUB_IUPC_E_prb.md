## E. Helping Knuth

**Limits:** 1s, 256 MB

Professor Raj Chandra Bose asked Donald Knuth to complete a partially known permutation.

You are given an array `a` of length `n`. Some positions contain known values, while missing values are represented by `-1`.

Your task is to replace every `-1` with a distinct value from `1` to `n` so that:

1. The final array becomes a valid permutation of `1...n`.
2. The value of

[
\sum_{i=2}^{n}(a_i-a_{i-1})
]

is minimized.

If multiple optimal permutations exist, output any of them.

### Observation

The objective simplifies dramatically:

[
(a_2-a_1)+(a_3-a_2)+\cdots+(a_n-a_{n-1})
]

All middle terms cancel out, leaving

[
a_n-a_1
]

So we only need to minimize `a[n] - a[1]`.

Let `U` be the set of unused numbers.

* If both endpoints are fixed, the answer is already determined.
* If `a[1] = -1`, assign the **largest** unused number to position `1`.
* If `a[n] = -1`, assign the **smallest** unused number to position `n`.
* If both endpoints are missing, assign:

  * largest unused number to position `1`
  * smallest unused number to position `n`

This minimizes `a[n] - a[1]`.

After fixing the endpoints, fill all remaining `-1` positions with any remaining unused numbers.

### Complexity

Each test case uses a set of unused values and performs `O(n log n)` operations.

## Solve(C++)

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    ios::sync_with_stdio(false);
    cin.tie(nullptr);

    int T;
    cin >> T;
    while(T--){
        int n;
        cin >> n;
        vector<int> a(n);
        vector<int> used(n + 1, 0);
        for(int i = 0; i < n; i++){
            cin >> a[i];
            if (a[i] != -1) used[a[i]] = 1;
        }
        set<int> rem;
        for(int x = 1; x <= n; x++){
            if(!used[x]) rem.insert(x);
        }
        bool firstMissing = (a[0] == -1);
        bool lastMissing  = (a[n - 1] == -1);
        if(firstMissing && lastMissing){
            int mx = *rem.rbegin();
            a[0] = mx;
            rem.erase(mx);
            int mn = *rem.begin();
            a[n - 1] = mn;
            rem.erase(mn);
        }
        else if(firstMissing){
            int mx = *rem.rbegin();
            a[0] = mx;
            rem.erase(mx);
        }
        else if(lastMissing){
            int mn = *rem.begin();
            a[n - 1] = mn;
            rem.erase(mn);
        }
        for(int i = 0; i < n; i++){
            if(a[i] == -1){
                a[i] = *rem.begin();
                rem.erase(rem.begin());
            }
        }
        for(int i = 0; i < n; i++){
            if (i) cout << ' ';
            cout << a[i];
        }
        cout << endl;
    }
}
```
