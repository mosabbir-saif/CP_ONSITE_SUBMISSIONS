## D. Toggle The Streetlights

**Limits:** 1s, 256 MB

The Metropolitan University campus has a long street with `n` streetlights arranged in a row, numbered from `1` to `n`. Each streetlight is either on (`1`) or off (`0`).

Every minute, all streetlights are updated simultaneously according to the following rule:

* For a streetlight at position `i`, its neighbors are positions `i-1` and `i+1` if they exist.
* A streetlight toggles its state (`0 → 1` or `1 → 0`) **if and only if** it has exactly two neighbors and both neighbors were on in the previous minute.

Given the initial configuration, determine the state of all streetlights after exactly `k` minutes.

### Input

The first line contains an integer `T` (`1 ≤ T ≤ 10^5`) — the number of test cases.

For each test case:

* The first line contains two integers `n` and `k` (`1 ≤ n ≤ 10^5`, `0 ≤ k ≤ 10^9`).
* The second line contains a binary string `s` of length `n`.

It is guaranteed that the sum of `n` over all test cases does not exceed `10^6`.

### Output

For each test case, print the configuration after exactly `k` minutes.

### Example

| Input | Output |
| ----- | ------ |
| 1     |        |
| 5 1   | 01110  |
| 01010 |        |

### Observation

Only positions `2 ... n-1` can ever change because endpoints do not have two neighbors.

For an interior position `i`:

```
next[i] = current[i] XOR (current[i-1] & current[i+1])
```

Let:

```
f(x) = x XOR (L & R)
```

where `L` and `R` are the left and right neighbors.

Applying the operation twice:

```
f(f(x))
= (x XOR (L & R)) XOR (L & R)
= x
```

Therefore every affected cell alternates between two states, and the entire system has period `2`.

So:

* `k = 0` → original string.
* `k` odd → apply the transformation once.
* `k` even and `k > 0` → the configuration returns to the original string.

Thus we only need at most one simulation step.

## Solve(C++)

```cpp
#include<bits/stdc++.h>
#define ll long long
using namespace std;

signed main(){
    ll tc; 
    cin >> tc;
    while(tc--){
        ll n,m; 
        cin >> n >> m;
	string s, a; 
	cin >> s;
	a = s;
        ll cnt = 0;
        if(m == 0 || n < 3){
            cout << s << endl;
            continue;
        }
        if(m&1){
            for(ll k = 0; k < 11 && k < m; k++){
        	for(ll i = 1; i < n - 1; i++){
            	    if(s[i - 1] == '1' && s[i + 1] == '1'){
                	if(s[i] == '0') a[i] = '1';
                	else a[i] = '0';
               	    }
                }
        	s = a;
            }
            cout << a << endl;
	}
        else{
            for(ll k = 0; k < 10 && k < m; k++){
                for(ll i = 1; i < n - 1; i++){
                    if(s[i - 1] == '1' && s[i + 1] == '1'){
                        if(s[i] == '0') a[i] = '1';
                        else a[i] = '0';
                    }
                }
        	s = a;
            } 
            cout << a << endl;
        }
    }
}
```
