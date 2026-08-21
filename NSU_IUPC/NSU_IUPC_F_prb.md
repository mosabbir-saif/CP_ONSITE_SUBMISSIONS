# F. Fool's Gold

**Time limit per test:** 3 seconds  
**Memory limit per test:** 256 MB

## Problem Statement

In the Kingdom of Chemistry, every citizen has a unique elemental ID ranging from `1` to `n`. King Pyrite, whose elemental ID is `n`, rules over the kingdom with an aura of false purity.

To solidify his rule, the king seeks to form an elite council known as *The Noble Catalysts*. These individuals will be publicly regarded as the most brilliant minds in the kingdom, yet their true purpose is not to provide wisdom but to accelerate the king's plans without resistance. Like chemical catalysts, they thrive under King Pyrite's influence, ensuring that his decrees are swiftly accepted by the people without question.

The king has two strict criteria for selecting his advisors:

*Loyalty* — An advisor must always agree with the king's decisions.
*Credibility* — The citizens must never doubt the intelligence or capabilities of the chosen advisors.
The kingdom's Royal Alchemist has prophesied that for two citizens with elemental IDs `x` and `y` where `x<y`, the person with ID `x` will always agree with the person with ID `y` if the following condition holds:

```
gcd(x,y)+lcm(x,y)=x+y
```

Here `gcd(x,y)` denotes the greatest common divisor of `x` and `y`, and `lcm(x,y)` denotes the least common multiple of `x` and `y`.

However, there is a catch. To maintain the illusion of a flawless selection, King Pyrite will only invite citizens whose elemental ID is a perfect square, as these individuals are perceived as the "*purest*" in the kingdom.

Given the value of `n`, determine how many citizens can be selected as advisors by King Pyrite such that all of the following conditions hold:

They will always agree with the king. `x` is a perfect square. `x<n` (the king himself cannot be an advisor).

## Input
The first line of the input contains a single integer `t` (`1≤t≤10^5`) — the number of test cases.

Each test case consists of a single line containing a single integer `n` (`2≤n≤10^9`) — the number of citizens.

## Output

For each test case, output a single integer in a line — the number of citizens that can be selected as advisors.

## Examples

**Input**
```text
4
10
16
25
100000000
```

**Output**
```text
1
2
1
24
```

## Solve(c++)
```cpp
#include <bits/stdc++.h>
using namespace std;

typedef long long ll;

vector<int> primes;

void sieve(int n) {
    vector<bool> is_prime(n + 1, true);
    is_prime[0] = is_prime[1] = false;
    for (int i = 2; i * i <= n; i++) {
        if (is_prime[i]) {
            for (int j = i * i; j <= n; j += i) {
                is_prime[j] = false;
            }
        }
    }
    for (int i = 2; i <= n; i++) {
        if (is_prime[i]) primes.push_back(i);
    }
}

int main() {
    ios::sync_with_stdio(false);
    cin.tie(nullptr);
    
    sieve(31623);  // sqrt(1e9) ≈ 31623
    
    int t;
    cin >> t;
    while (t--) {
        int n;
        cin >> n;
        
        int temp = n;
        ll ans = 1;
        bool is_perfect_square = true;
        
        for (int p : primes) {
            if (1LL * p * p > temp) break;
            if (temp % p == 0) {
                int e = 0;
                while (temp % p == 0) {
                    temp /= p;
                    e++;
                }
                ans *= (e / 2 + 1);
                if (e % 2 != 0) is_perfect_square = false;
            }
        }
        
        if (temp > 1) {  // remaining prime factor
            is_perfect_square = false;
        }
        
        if (is_perfect_square) ans--;
        
        cout << ans << '\n';
    }
    return 0;
}
```