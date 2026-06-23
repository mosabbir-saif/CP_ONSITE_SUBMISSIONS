## C. Max Person

**Limits:** 1s, 256 MB

You have an infinite-storey building. Each floor has exactly `n` rooms, and each room can accommodate one person.

Placing one person on floor `x` (where floors are 1-indexed: `x = 1, 2, 3, …`) costs `2^x` units of budget. You are given a total budget of `m` and you must spend all of it.

Your task is to determine the maximum possible number of people you can accommodate while spending exactly `m`. If it is impossible to spend the budget exactly, output `-1`.

### Input

The first line contains an integer `T` (1 ≤ T ≤ 10^5) — the number of test cases.

Each of the next `T` lines contains two integers `n` (1 ≤ n ≤ 10^18) and `m` (1 ≤ m ≤ 10^18).

### Output

For each test case, print a single integer on its own line — the maximum number of people that can be accommodated while spending exactly `m`, or `-1` if it is impossible.

### Example

| Input | Output |
|-------|--------|
| 2 | |
| 5 10 | 5 |
| 1 30 | 4 |

**Case 1:** n = 5, m = 10. Place 5 people on floor 1. Cost: 5 × 2^1 = 10 ✓ Answer: 5

**Case 2:** n = 1, m = 30. Place one person on floors 1, 2, 3, 4. Cost: 2 + 4 + 8 + 16 = 30. Total people: 4



## Solve(c++)

```cpp
#include<bits/stdc++.h>
using namespace std;
#define int long long
signed main(){
	int t; cin >> t;
	while(t--){
		int  n, m;
		cin >> n >> m;
		int cnt = 0;int i=1;
		int z =-1, ct2 = 0, flr;
		if(m&1){
			cout << "-1" << endl;
			continue;
		}
		for(;i<=70; i++)
		{
			int x = n * (1LL<<i);
			int y = (1LL<<i);
			if(m>=x)
			{
				m-=x;
				cnt+=n;
			}
			else if (m>=y){
			    z= m/y;
				cnt+=z;
				m-=z*y;
                break;
			}
			else if((1LL<<i) > m){
                break;
			}

		}
		if(m == 0) cout << cnt << endl;
		else{
		int need = (z == n) ? (1LL<<(i+1)) : (1LL << i);
		need -= m;
		if(z == n) flr = i;
		else flr = i-1;
		while(need > 0){
            int dig = need/(1LL<<flr);
            need -= (dig*(1LL<<flr));
            ct2+=dig;
            flr--;
		}
		cout<<cnt-ct2+1LL<<endl;}
	}
}
```