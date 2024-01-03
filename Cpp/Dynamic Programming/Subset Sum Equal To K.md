### [Subset Sum Equal To K]()

## Explanation:

## Time and Space Complexity:
### `Time Complexity`:

### `Space Complexity`:

## Tabulization:
```cpp
#include <bits/stdc++.h> 

// Function to check if there exists a subset with the sum equal to k
bool subsetSumToK(int n, int k, vector<int> &arr) {
    // Create a 2D DP array to store subproblem solutions
    vector<vector<bool>> dp(n, vector<bool>(k + 1, 0));

    // Set the base case: if target sum is 0, there is always an empty subset
    for (int i = 0; i < n; i++)
        dp[i][0] = true;

    // Set the base case: if the first element is equal to the target, set it to true
    if (arr[0] <= k) dp[0][arr[0]] = true;

    // Dynamic Programming approach to solve the subset sum problem
    for (int ind = 1; ind < n; ind++) {
        for (int target = 1; target <= k; target++) {
            // If we choose not to take the current element
            bool notTake = dp[ind - 1][target];

            // If we choose to take the current element (if it is less than or equal to the target)
            bool take = false;
            if (target >= arr[ind])
                take = dp[ind - 1][target - arr[ind]];

            // Update the DP table with the result of taking or not taking the current element
            dp[ind][target] = take || notTake;
        }
    }

    // The final result is stored in the bottom-right cell of the DP table
    return dp[n - 1][k];
}

```

## Recursion:
```cpp
#include <bits/stdc++.h> 

// Function to check if there exists a subset with the given target sum
bool subsetUtil(int ind, int target, vector<int> &arr) {
    // Base case: if the target sum is 0, the subset is found
    if (target == 0) return true;

    // Base case: if we have reached the first element and it is equal to the target, return true
    if (ind == 0) return arr[ind] == target;

    // Recursive case: Try not taking the current element in the subset
    bool notTake = subsetUtil(ind - 1, target, arr);

    // Recursive case: Try taking the current element in the subset if it is less than or equal to the target
    bool take = false;
    if (target >= arr[ind]) {
        take = subsetUtil(ind - 1, target - arr[ind], arr);
    }

    // Return true if either notTake or take is true
    return take || notTake;
}

// Function to check if there exists a subset with the sum equal to k
bool subsetSumToK(int n, int k, vector<int> &arr) {
    // Call the subsetUtil function to check for the subset
    return subsetUtil(n, k, arr);
}

```
