## K. Diagonal Shortcuts

**Limits:** 1s, 256 MB

Upobir starts at `(0,0)` on an infinite chessboard and wants to reach `(x,x)`.

He has two possible actions:

1. **Knight Move** (cost = 1):

   * `(±1, ±2)` or `(±2, ±1)` as in chess.

2. **Special Jump** (cost = `k`):

   * Instantly teleport from the current position directly to `(x,x)`.

Find the minimum energy required.


## Solve(C++)

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    ios::sync_with_stdio(false);
    cin.tie(nullptr);

    int t;
    cin >> t;
    while(t--){
        long long x, k;
        cin >> x >> k;
        long long knight;
        if(x == 1) knight = 2;
        else if(x == 2) knight = 4;
        else knight = 2 * ((x + 2) / 3);
        cout << min(knight, k) << endl;
    }
}
```
