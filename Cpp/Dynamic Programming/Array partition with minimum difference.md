### [Array partition with minimum difference](https://www.codingninjas.com/studio/problems/partition-a-set-into-two-subsets-such-that-the-difference-of-subset-sums-is-minimum_842494?source=youtube&campaign=striver_dp_videos&utm_source=youtube&utm_medium=affiliate&utm_campaign=striver_dp_videos&leftPanelTabValue=PROBLEM)

## Explanation:
Sure, let's break down the code:

1. **Function Definition**: The function `minSubsetSumDifference` is defined with two parameters - a vector `arr` representing the array, and an integer `n` representing the size of the array.

2. **Total Sum Calculation**: The total sum of the array elements is calculated and stored in `totalSum`.

3. **Target Sum**: The target sum for the subset is set as the total sum of the array.

4. **DP Table Initialization**: A 2D dynamic programming (DP) table is initialized. The size of the table is `n x (targetSum + 1)`. Each cell `dp[i][j]` in the table represents whether it is possible to achieve a sum `j` using the first `i` elements of the array.

5. **Base Cases**: The base cases for the DP table are set. If the sum is 0, it is always possible to achieve it (by taking no elements), so `dp[i][0]` is set to `true` for all `i`. If the first element of the array is less than or equal to the target sum, `dp[0][arr[0]]` is set to `true`.

6. **DP Table Filling**: The DP table is filled using a nested loop. For each element at index `ind`, and for each possible sum `subsetSum`, two possibilities are considered - taking the current element (`take`), and not taking the current element (`notTake`). The result for `dp[ind][subsetSum]` is updated as the logical OR of these two possibilities.

7. **Minimum Difference Calculation**: The minimum subset sum difference is calculated by iterating through the second half of the total sum. For each possible sum `s1`, if it is achievable (`dp[n-1][s1]` is `true`), the absolute difference between `s1` and the remaining sum `(totalSum - s1)` is calculated. The minimum of this difference and the current minimum difference is updated as the new minimum difference.

8. **Return Value**: The function returns the calculated minimum subset sum difference.

## Time and Space Complexity:
### `Time Complexity`: 
The time complexity of this code is **O(n * totalSum)**, where **n** is the number of elements in the array, and **totalSum** is the total sum of the array elements. This is because each cell in the DP table is filled once.

### `Space Complexity`:
The space complexity of this code is also **O(n * totalSum)**. This is because a 2D DP table of size `n x (totalSum + 1)` is used.

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
