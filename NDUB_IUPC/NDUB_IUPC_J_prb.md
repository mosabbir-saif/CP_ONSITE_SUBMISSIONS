## F. Stable Gears

**Limits:** 1s, 256 MB

In the Lalbagh Fort locking mechanism, the number of gears installed after `k` days is:

[
n = 1 + 3 + 5 + \cdots + (2k-1) = k^2
]

The gears are numbered `1, 2, ..., n`, and gear `x` has exactly `x` teeth.

A gear is considered **stable** if the number of divisors of `x` that are even equals the number of divisors of `x` that are odd.

Given `k`, determine how many stable gears exist among gears `1` through `k²`.

### Observation

Let

[
x = 2^a \cdot m
]

where `m` is odd.

The number of odd divisors of `x` is:

[
d(m)
]

since an odd divisor cannot contain any factor of `2`.

The total number of divisors is:

[
(a+1)d(m)
]

Therefore the number of even divisors is:

[
(a+1)d(m)-d(m)=a,d(m)
]

For stability:

[
a,d(m)=d(m)
]

Since `d(m) > 0`, we get:

[
a=1
]

Thus a gear is stable **iff it is divisible by 2 but not by 4**, i.e.

[
v_2(x)=1
]

So we only need to count numbers in `[1, k²]` that are multiples of `2` but not multiples of `4`.

The count is:

[
\left\lfloor \frac{k^2}{2} \right\rfloor -
\left\lfloor \frac{k^2}{4} \right\rfloor
]

### Complexity

`O(1)` per test case.

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
