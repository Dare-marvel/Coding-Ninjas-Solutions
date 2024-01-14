### [0 1 Knapsack](https://www.codingninjas.com/studio/problems/0-1-knapsack_920542?source=youtube&campaign=striver_dp_videos&utm_source=youtube&utm_medium=affiliate&utm_campaign=striver_dp_videos)

## Explanation:

## Time and Space Complexity:
### `Time Complexity`:

### `Space Complexity`:

## Code:
```cpp

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
