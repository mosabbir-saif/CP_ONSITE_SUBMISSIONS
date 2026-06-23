## K. Diagonal Shortcuts

**Limits:** 1s, 256 MB

Upobir starts at `(0,0)` on an infinite chessboard and wants to reach `(x,x)`.

He has two possible actions:

1. **Knight Move** (cost = 1):

   * `(±1, ±2)` or `(±2, ±1)` as in chess.

2. **Special Jump** (cost = `k`):

   * Instantly teleport from the current position directly to `(x,x)`.

Find the minimum energy required.

### Observation

Using the special jump after making some knight moves is never beneficial.

If Upobir plans to use the jump, he should simply use it immediately from `(0,0)`, costing exactly `k`.

Therefore the answer is:

[
\min(k,\text{KnightDistance}((0,0),(x,x)))
]

So we only need the knight distance to `(x,x)`.

### Knight Distance on the Diagonal

A pair of knight moves

[
(1,2) + (2,1)
]

moves the knight from `(a,a)` to `(a+3,a+3)` in exactly **2 moves**.

Hence every increase of `3` along the diagonal costs `2` moves.

This gives:

* `x = 1` → distance = `2`
* `x = 2` → distance = `4`
* `x ≥ 3` →

[
\text{dist}(x,x)=2\left\lceil \frac{x}{3}\right\rceil
]

Checking small values:

| x | distance |
| - | -------- |
| 1 | 2        |
| 2 | 4        |
| 3 | 2        |
| 4 | 4        |
| 5 | 4        |
| 6 | 4        |
| 7 | 6        |

which matches the formula.

Therefore:

[
\text{answer}
=============

\min\left(
k,
\begin{cases}
2,&x=1\
4,&x=2\
2\left\lceil \frac{x}{3}\right\rceil,&x\ge3
\end{cases}
\right)
]

### Complexity

`O(1)` per test case.

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
