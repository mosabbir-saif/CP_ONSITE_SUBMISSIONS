## B. Divisible Substrings

**Limits:** 1s, 256 MB

You are given a digit string `s` of length `n`, where each character is a digit from `1` to `9`.

For every pair of indices `1 ≤ i ≤ j ≤ n`, consider the number formed by the contiguous substring `s[i...j]`. Your task is to determine whether **every** such substring is divisible by its length `(j - i + 1)`.

Print `YES` if the condition holds for all substrings, otherwise print `NO`.

### Input

The first line contains an integer `t` (`1 ≤ t ≤ 10^4`) — the number of test cases.

For each test case:

* The first line contains an integer `n` (`1 ≤ n ≤ 3·10^5`) — the length of the string.
* The second line contains a string `s` of length `n` consisting only of digits from `1` to `9`.

It is guaranteed that the sum of `n` over all test cases does not exceed `3·10^5`.

### Output

For each test case, print `YES` if every substring is divisible by its length, otherwise print `NO`.

### Example

| Input | Output |
| ----- | ------ |
| 3     |        |
| 3     | YES    |
| 162   |        |
| 2     | NO     |
| 69    |        |
| 1     | YES    |
| 7     |        |

### Observation

If a string has length at least `5`, then it must contain a substring of length `5`.

A number divisible by `5` must end with `0` or `5`. Since digits are restricted to `1..9`, it must end with `5`.

However, every substring of length `2` must also be divisible by `2`, which means every digit except possibly the first must be even.

A digit cannot be both `5` and even, so no valid string can have length `5` or greater.

Therefore:

* If `n ≥ 5`, the answer is immediately `NO`.
* Otherwise (`n ≤ 4`), we can brute-force all substrings and check divisibility directly.

## Solve(C++)

```cpp
#include <bits/stdc++.h>
#define int long long
using namespace std;

signed main() {
    ios::sync_with_stdio(false);
    cin.tie(nullptr);

    int t;
    cin >> t;
    while(t--){
        int n;
        string s;
        cin >> n >> s;
        if(n >= 5){
            cout << "NO" << endl;
            continue;
        }
        bool ok = true;
        for(int i = 0; i < n && ok; i++){
            long long num = 0;
            for(int j = i; j < n; j++){
                num = num * 10 + (s[j] - '0');
                int len = j - i + 1;
                if(num % len != 0){
                    ok = false;
                    break;
                }
            }
        }

        cout << (ok ? "YES" : "NO") << endl;
    }
}
```
