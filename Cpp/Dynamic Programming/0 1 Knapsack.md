### [0 1 Knapsack](https://www.codingninjas.com/studio/problems/0-1-knapsack_920542?source=youtube&campaign=striver_dp_videos&utm_source=youtube&utm_medium=affiliate&utm_campaign=striver_dp_videos)

## Explanation:

## Time and Space Complexity:
### `Time Complexity`:

### `Space Complexity`:

## Tabulation:
```cpp
#include <bits/stdc++.h>
using namespace std;

// Function to solve the 0/1 Knapsack problem using dynamic programming
int knapsack(vector<int>& wt, vector<int>& val, int n, int W) {
    // Create a 2D DP table with dimensions n x W+1 and initialize it with zeros
    vector<vector<int>> dp(n, vector<int>(W + 1, 0));

    // Base condition: Fill in the first row for the weight of the first item
    for (int i = wt[0]; i <= W; i++) {
        dp[0][i] = val[0];
    }

    // Fill in the DP table using a bottom-up approach
    for (int ind = 1; ind < n; ind++) {
        for (int cap = 0; cap <= W; cap++) {
            // Calculate the maximum value by either excluding the current item or including it
            int notTaken = dp[ind - 1][cap];
            int taken = INT_MIN;

            // Check if the current item can be included without exceeding the knapsack's capacity
            if (wt[ind] <= cap) {
                taken = val[ind] + dp[ind - 1][cap - wt[ind]];
            }

            // Update the DP table
            dp[ind][cap] = max(notTaken, taken);
        }
    }

    // The final result is in the last cell of the DP table
    return dp[n - 1][W];
}
```

## Memoization:
```cpp
#include <bits/stdc++.h> 

int knapUtil(vector<int> weight,vector<int> value,int n, int maxWeight,int remWt,int ind, vector<vector<int>> &dp){
	if(ind == 0){
		if(weight[0] <= remWt) return value[0];
		else return 0;
	}

	if(dp[ind][remWt] != -1) return dp[ind][remWt];

	int notTake = knapUtil(weight, value, n, maxWeight, remWt,ind-1,dp);

	int take = INT_MIN;
	if(weight[ind] <= remWt) take = value[ind] + knapUtil(weight, value, n, maxWeight, remWt-weight[ind], ind-1,dp);

	return dp[ind][remWt] = max(take,notTake);
}
int knapsack(vector<int> weight, vector<int> value, int n, int maxWeight) 
{
	vector<vector<int>> dp(n, vector<int>(maxWeight + 1, -1));
	return knapUtil(weight, value, n, maxWeight, maxWeight, n-1,dp);
}
```

## Recursion:
```cpp
#include <bits/stdc++.h> 

int knapUtil(vector<int> weight,vector<int> value,int n, int maxWeight,int remWt,int ind){
	if(ind == 0){
		if(weight[0] <= remWt) return value[0];
		else return 0;
	}

	int notTake = knapUtil(weight, value, n, maxWeight, remWt,ind-1);

	int take = INT_MIN;
	if(weight[ind] <= remWt) take = value[ind] + knapUtil(weight, value, n, maxWeight, remWt-weight[ind], ind-1);

	return max(take,notTake);
}
int knapsack(vector<int> weight, vector<int> value, int n, int maxWeight) 
{
	return knapUtil(weight, value, n, maxWeight, maxWeight, n-1);
}
```
