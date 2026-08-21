## F. Stable Gears

**Limits:** 1s, 256 MB

In the heart of 17th-century Dhaka, the construction of the Lalbagh Fort is underway. To secure the southern gate, the royal architect has designed a complex locking mechanism consisting of `n` interlocking brass gears.

The total number of gears, `n`, is determined by the number of days `k` spent on the gate's construction. On the `1st` day, `1` gear was installed. On each subsequent day, the builders added the next consecutive odd number of gears (3 on the second day, 5 on the third, and so on).

Each gear in the system is unique, numbered `1,2,…,n`. A gear numbered `x` has exactly `x` teeth. For the mechanism to rotate without friction, the architect only selects gears that are mechanically stable.

The stability of a gear is determined by its rotational partitions. A gear with `x` teeth can be partitioned into `m` equal-sized segments, where `m` is any integer that divides `x`. A gear is mechanically stable only if the number of ways to partition it into segments containing an even number of teeth is perfectly balanced by the number of ways to partition it into segments containing an odd number of teeth.

For example, consider gear `6`. It can be partitioned into segments of size `1, 2, 3, or 6`.

Segments of size `2` and `6` are even-sized.
Segments of size `1` and `3` are odd-sized.
Since there are exactly two even-sized partition options and two odd-sized partition options, gear `6` is stable.

Given the number of construction days `k`, calculate how many mechanically stable gears are in the Lalbagh gate.

# Input
The first line contains a single integer `t` (`1≤t≤10^6`) — the number of test cases.

Each of the next `t` lines contains a single integer `k` (`1≤k≤2^32`) — the number of construction days.

# Output
For each test case, output a single integer — the number of mechanically stable gears among all gears numbered from `1` to `n`.

# Example
|Input|Output|
|-----|------|
| 4 | |
| 1 | 0 |
| 2 | 1 |
| 5 | 6 |
| 10 | 25 |


## Solve(C++)

```cpp
#include <bits/stdc++.h>
using namespace std;

void print128(__int128 x){
    if(x == 0){
        cout << 0;
        return;
    }
    string s;
    while(x){
        s.push_back('0' + x % 10);
        x /= 10;
    }
    reverse(s.begin(), s.end());
    cout << s;
}

int main() {
    ios::sync_with_stdio(false);
    cin.tie(nullptr);

    int t;
    cin >> t;
    while(t--){
        int k;
        cin >> k;
        __int128 N = (__int128)k * k;
        __int128 ans = N / 2 - N / 4;
        print128(ans);
        cout << endl;
    }
}
```
