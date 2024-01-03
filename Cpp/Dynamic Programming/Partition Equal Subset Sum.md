### [Partition Equal Subset Sum](https://www.codingninjas.com/studio/problems/partition-equal-subset-sum_892980?source=youtube&campaign=striver_dp_videos&utm_source=youtube&utm_medium=affiliate&utm_campaign=striver_dp_videos&leftPanelTabValue=PROBLEM)

## Explanation:

## Time and Space Complexity:
### `Time Complexity`:

### `Space Complexity`:

## Tabulization:
```cpp
bool subsetSumUtil(int ind, int target, vector<int>& arr, vector<vector<int>>& dp) {
    // Base case: If the target sum is 0, we found a valid partition
    if (target == 0)
        return true;

    // Base case: If we have considered all elements and the target is still not 0, return false
    if (ind == 0)
        return arr[0] == target;

    // If the result for this state is already calculated, return it
    if (dp[ind][target] != -1)
        return dp[ind][target];

    // Recursive cases
    // 1. Exclude the current element
    bool notTaken = subsetSumUtil(ind - 1, target, arr, dp);

    // 2. Include the current element if it doesn't exceed the target
    bool taken = false;
    if (arr[ind] <= target)
        taken = subsetSumUtil(ind - 1, target - arr[ind], arr, dp);

    // Store the result in the DP table and return
    return dp[ind][target] = notTaken || taken;
}

bool canPartition(vector<int> &arr, int n)
{
	int totSum = 0;

    // Calculate the total sum of the array
    for (int i = 0; i < n; i++) {
        totSum += arr[i];
    }

    // If the total sum is odd, it cannot be partitioned into two equal subsets
    if (totSum % 2 == 1)
        return false;
    else {
        int k = totSum / 2;

        // Create a DP table with dimensions n x k+1 and initialize with -1
        vector<vector<int>> dp(n, vector<int>(k + 1, -1));

        // Call the subsetSumUtil function to check if it's possible to partition
        return subsetSumUtil(n - 1, k, arr, dp);
    }
}

```
