### [Unbounded Knapsack](https://www.codingninjas.com/studio/problems/unbounded-knapsack_1215029?source=youtube&campaign=striver_dp_videos&utm_source=youtube&utm_medium=affiliate&utm_campaign=striver_dp_videos)

## [Explanation](https://takeuforward.org/data-structure/unbounded-knapsack-dp-23/):

## Tabulation:
```cpp
#include <climits>
#include <vector>

int unboundedKnapsack(int n, int w, vector<int> &profit, vector<int> &weight){
    vector<vector<int>> dp(n,vector<int>(w+1,0));
    
    for(int W=0;W<=w;W++) dp[0][W] = (W/weight[0])*profit[0];

    for(int ind=1;ind<n;ind++){
        for(int wt=0;wt<=w;wt++){
            int notTAke = dp[ind-1][wt];
            int take = INT_MIN;
            if(weight[ind] <= wt) take = profit[ind] + dp[ind][wt-weight[ind]];

            dp[ind][wt] = max(take,notTAke);
        }
    }

    return dp[n-1][w];
}
```

## Memoization:
```cpp
#include <climits>
#include <vector>

int unboundedKnapsackHelper(vector<int> &profit, vector<int> &weight, int remWt, int ind,vector<vector<int>> &dp){
    if(ind == 0) return (remWt/weight[ind])*profit[ind];

    if(dp[ind][remWt] != -1) return dp[ind][remWt];

    int notTAke = unboundedKnapsackHelper(profit, weight, remWt, ind-1,dp);
    int take = INT_MIN;
    if(weight[ind] <= remWt) take = profit[ind] + unboundedKnapsackHelper(profit, weight, remWt-weight[ind], ind,dp);

    return dp[ind][remWt] = max(take,notTAke);
}

int unboundedKnapsack(int n, int w, vector<int> &profit, vector<int> &weight){
    vector<vector<int>> dp(n,vector<int>(w+1,-1));
    return unboundedKnapsackHelper(profit, weight, w, n-1,dp);
}
```

## Recursion:
```cpp
#include <climits>
#include <vector>

int unboundedKnapsackHelper(vector<int> &profit, vector<int> &weight, int remWt, int ind){
    if(ind == 0) return (remWt/weight[ind])*profit[ind];

    int notTAke = unboundedKnapsackHelper(profit, weight, remWt, ind-1);
    int take = INT_MIN;
    if(weight[ind] <= remWt) take = profit[ind] + unboundedKnapsackHelper(profit, weight, remWt-weight[ind], ind);

    return max(take,notTAke);
}

int unboundedKnapsack(int n, int w, vector<int> &profit, vector<int> &weight){
    return unboundedKnapsackHelper(profit, weight, w, n-1);
}
```
