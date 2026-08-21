## K. Diagonal Shortcuts

**Limits:** 1s, 256 MB

Upobir is playing a game on an infinite `2D` grid. He starts at the origin `(0,0)` and wants to travel to the target coordinate `(x,x)`. To navigate the grid, Upobir can perform two types of moves:

Chess Knight Move: 
From his current position `(x1,y1)`, he can move to any coordinate `(x2,y2)` such that `|x1−x2|=1` and `|y1−y2|=2`, or `|x1−x2|=2` and `|y1−y2|=1`. This move costs 1 unit of energy.
Special Jump: He can perform a unique jump to instantly teleport from his `current` position directly to the target `(x,x)`. This unique move does not follow standard chess rules and costs `k` units of energy.
Given `x` and `k, find the minimum total energy Upobir needs to spend to reach `(x,x)`.

# Input
The first line contains a single integer `t` (`1≤t≤10^5`) — the number of test cases.

The only line of each test case contains two integers `x` and `k` (`1≤x≤10^9, 1≤k≤10^9`) — the coordinate value defining the target `(x,x)`, and the energy cost of the special jump.

# Output
For each test case, print a single integer — the minimum total energy required to reach `(x,x)`.

**Example**
|Input|Output|
|-----|------|
| 3 | |
| 1 5 | 2 |
| 3 2 | 2 |
| 3 3 | 2 |


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
