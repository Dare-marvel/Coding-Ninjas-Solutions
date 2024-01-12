### [Partitions With Given Difference](https://www.codingninjas.com/studio/problems/partitions-with-given-difference_3751628?source=youtube&campaign=striver_dp_videos&utm_source=youtube&utm_medium=affiliate&utm_campaign=striver_dp_videos&leftPanelTabValue=PROBLEM)

## Explanation:

## Time and Space Complexity:
### `Time Complexity`:

### `Space Complexity`:

## Tabulization:
```cpp
#include <bits/stdc++.h> 
int mod = (1e9 + 7);

// Function to count the number of subsets with a given sum
int findWays(vector<int>& num, int k) {
    int n = num.size();

    // Create a 2D DP table with dimensions n x k+1, initialized with zeros
    vector<vector<int>> dp(n, vector<int>(k + 1, 0));

    if(num[0] == 0) dp[0][0] = 2;
    else dp[0][0] = 1;


    // Initialize the first row based on the first element of the array
    if (num[0] != 0 && num[0] <= k) {
        dp[0][num[0]] = 1;
    }

    // Fill in the DP table using a bottom-up approach
    for (int ind = 1; ind < n; ind++) {
        for (int target = 0; target <= k; target++) {
            // Exclude the current element
            int notTaken = dp[ind - 1][target];

            // Include the current element if it doesn't exceed the target
            int taken = 0;
            if (num[ind] <= target) {
                taken = dp[ind - 1][target - num[ind]];
            }

            // Update the DP table
            dp[ind][target] = (notTaken + taken) % mod;
        }
    }

    // The final result is in the last cell of the DP table
    return dp[n - 1][k];
}


int countPartitions(int n, int d, vector<int> &arr) {
    // Write your code here.
    int totSum = 0;
    for(auto &it: arr) totSum+= it;
    if(totSum - d < 0 || (totSum - d) % 2) return 0;
    return findWays(arr, (totSum - d) / 2);
}
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
