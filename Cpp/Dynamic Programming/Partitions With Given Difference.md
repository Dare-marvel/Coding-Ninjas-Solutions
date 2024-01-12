### [Partitions With Given Difference]()

## Explanation:

## Time and Space Complexity:
### `Time Complexity`:

### `Space Complexity`:

## Code:
```

```

## Memoization:
```cpp
#include <bits/stdc++.h> 
int mod = (1e9 + 7);

int findWaysUtil(int ind, int target, vector<int>& arr, vector<vector<int>>& dp) {

    
    if (ind == 0){
        if(target == 0 && arr[0] == 0) return 2;
        if(target == 0 || target == arr[0]) return 1;
        return 0;
    }


    // If the result for this state is already calculated, return it
    if (dp[ind][target] != -1)
        return dp[ind][target];

    // Recursive cases
    // 1. Exclude the current element
    int notTaken = findWaysUtil(ind - 1, target, arr, dp);

    // 2. Include the current element if it doesn't exceed the target
    int taken = 0;
    if (arr[ind] <= target)
        taken = findWaysUtil(ind - 1, target - arr[ind], arr, dp);

    // Store the result in the DP table and return
    return dp[ind][target] = (notTaken + taken) % mod;
}

// Function to count the number of subsets with a given sum
int findWays(vector<int>& num, int k) {
    int n = num.size();
    vector<vector<int>> dp(n, vector<int>(k + 1, -1));
    return findWaysUtil(n - 1, k, num, dp);
}


int countPartitions(int n, int d, vector<int> &arr) {
    // Write your code here.
    int totSum = 0;
    for(auto &it: arr) totSum+= it;
    if(totSum - d < 0 || (totSum - d) % 2) return 0;
    return findWays(arr, (totSum - d) / 2);
}



```
