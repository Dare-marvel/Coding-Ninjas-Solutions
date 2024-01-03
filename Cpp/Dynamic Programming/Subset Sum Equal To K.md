### [Subset Sum Equal To K]()

## Explanation:

## Time and Space Complexity:
### `Time Complexity`:

### `Space Complexity`:

## Tabulization:
```cpp
#include <bits/stdc++.h> 

bool subsetSumToK(int n, int k, vector<int> &arr) {
    vector<vector<bool>> dp(n,vector<bool>(k+1,0));
    for (int i=0;i<n;i++) dp[i][0] = true;

    dp[0][arr[0]] = true;

    for(int ind=1;ind<n;ind++){
        for(int target=1;target<=k;target++){
            bool notTake = dp[ind-1][target];
            bool take = false;

            if(target >= arr[ind]) take = dp[ind-1][target-arr[ind]];
            dp[ind][target] = take || notTake;
        }
    }

    return dp[n-1][k];

}
```

## Recursion:
```cpp
#include <bits/stdc++.h> 

bool subsetUtil(int ind,int target,vector<int> &arr) {
    if (target == 0 ) return true;

    if ( ind == 0 ) return arr[ind] == target;

    bool notTake = subsetUtil(ind-1,target,arr);
    bool take = false;

    if(target >= arr[ind]) {
        take = subsetUtil(ind-1, target-arr[ind], arr);
    }

    return take || notTake;
}
bool subsetSumToK(int n, int k, vector<int> &arr) {
    // Write your code here.
    return subsetUtil(n,k,arr);
}
```
