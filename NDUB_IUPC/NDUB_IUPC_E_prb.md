## E. Helping Knuth

**Limits:** 1s, 256 MB

In the late 1950s, the renowned Bengali mathematician Professor Raj Chandra Bose was working to disprove Euler's long-standing conjecture on Latin Squares at Case Institute of Technology. During his visit, he noticed an exceptional undergraduate student attending his graduate level classes. Impressed by his ability, he invited the student, Donald Knuth, to assist with computational tasks.

As part of this work, Knuth needed to construct a `permutation` of length `n`, but only a partial version of the permutation is known.

He is given an array `a` of length `n`, where some elements are known and others are missing. Missing elements are represented by `−1`.

Your task is to help Knuth replace each occurrence of `−1` in `a` with a value from `1` to `n` such that:

The final array `a` becomes a valid permutation of integers from `1` to `n`.

The value of the following expression is minimized:

```
∑i=2n(ai − ai−1)
```
If multiple valid permutations achieve the minimum value, print any of them.

Note: A permutation of length `n` is an array of `n` distinct integers from `1` to `n`, each appearing exactly once. For example, 
`[1]`, `[4,3,5,1,2]` and `[3,2,1]` are permutations, while `[1,1]` and `[4,3,1]` are not.

# Input
The first line contains an integer `t` (`1≤t≤10^4`), the number of test cases. The description of the test cases follows.

For each test case, the first line contains an integer `n` (`2≤n≤2⋅10^5`), the length of the array.

The second line contains `n` integers `a1,a2,…,an`​  (`−1≤ai≤n, ai≠0`) , where `ai=−1` denotes a missing value.

It is guaranteed that all positive values in a are distinct.

The sum of `n` over all test cases does not exceed `2⋅10^5`.

# Output
For each test case, print a single line containing `n` space-separated integers, representing the completed permutation.

If there are multiple valid answers, print any of them.

## Example
**Input**
```
2
3
-1 3 -1
5
-1 2 -1 -1 3
```

**Output**
```
2 3 1 
5 2 4 1 3 
```

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
