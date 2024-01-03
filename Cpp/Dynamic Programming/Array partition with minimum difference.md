### [Array partition with minimum difference](https://www.codingninjas.com/studio/problems/partition-a-set-into-two-subsets-such-that-the-difference-of-subset-sums-is-minimum_842494?source=youtube&campaign=striver_dp_videos&utm_source=youtube&utm_medium=affiliate&utm_campaign=striver_dp_videos&leftPanelTabValue=PROBLEM)

## Explanation:

## Time and Space Complexity:
### `Time Complexity`:

### `Space Complexity`:

## Tabulization :
```cpp
// This function calculates the minimum subset sum difference using dynamic programming.

// Parameters:
// arr: The input vector representing the array.
// n: The size of the array.

int minSubsetSumDifference(vector<int>& arr, int n) {
    // Calculate the total sum of the array.
    int totalSum = 0;
    for(int i = 0; i < n; i++) {
        totalSum += arr[i];
    }

    // Set the upper bound for the subset sum.
    int targetSum = totalSum;

    // Initialize a 2D DP table to store the subset sum possibilities.
    vector<vector<bool>> dp(n, vector<bool>(targetSum + 1, false));

    // Base case: An empty subset can always achieve a sum of 0.
    for (int i = 0; i < n; i++) {
        dp[i][0] = true;
    }

    // Base case: If the first element is less than or equal to the target sum, set it to true.
    if (arr[0] <= targetSum) {
        dp[0][arr[0]] = true;
    }

    // Dynamic Programming approach to solve the subset sum problem
    for (int ind = 1; ind < n; ind++) {
        for (int subsetSum = 1; subsetSum <= targetSum; subsetSum++) {
            // If we choose not to take the current element.
            bool notTake = dp[ind - 1][subsetSum];

            // If we choose to take the current element (if it is less than or equal to the target sum).
            bool take = false;
            if (subsetSum >= arr[ind]) {
                take = dp[ind - 1][subsetSum - arr[ind]];
            }

            // Update the DP table with the result of taking or not taking the current element.
            dp[ind][subsetSum] = take || notTake;
        }
    }

    // Find the minimum subset sum difference by iterating through the second half of the total sum.
    int minDifference = 1e9;
    for(int s1 = 0; s1 <= totalSum / 2; s1++) {
        if(dp[n-1][s1] == true) {
            // Update the minimum difference using the absolute difference of subset sums.
            minDifference = min(minDifference, abs((totalSum - s1) - s1));
        }
    }

    // Return the calculated minimum subset sum difference.
    return minDifference;
}
```
