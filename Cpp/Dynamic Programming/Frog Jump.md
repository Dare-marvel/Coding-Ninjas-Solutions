### [Frog Jump](https://www.codingninjas.com/studio/problems/frog-jump_3621012)

## Explanation:

## Time and Space Complexity:
### `Time Complexity`:

### `Space Complexity`:

## Code:
## Recursion ( 3/5 test cases passed):
```cpp
#include <bits/stdc++.h> 

int helper(int ind,vector<int> &heights){
    if(ind == 0) return 0;

    int left = helper(ind-1,heights) + abs(heights[ind]-heights[ind-1]);
    int right = INT_MAX;
    if(ind > 1) right = helper(ind-2,heights) + abs(heights[ind]-heights[ind-2]);

    return min(left,right);
}
int frogJump(int n, vector<int> &heights)
{
    return helper(n-1,heights);   
}
```

## Dynamic Programming ( All test cases passed ):
```cpp
#include <bits/stdc++.h> 

int helper(int ind,vector<int> &heights,vector<int> &dp){
    if(ind == 0) return 0;

    if(dp[ind] != -1) return dp[ind];

    int left = helper(ind-1,heights,dp) + abs(heights[ind]-heights[ind-1]);
    int right = INT_MAX;
    if(ind > 1) right = helper(ind-2,heights,dp) + abs(heights[ind]-heights[ind-2]);

    return dp[ind]=min(left,right);
}
int frogJump(int n, vector<int> &heights)
{
    // Write your code here.
    vector<int> dp(n+1,-1);
    return helper(n-1,heights,dp);
    
}
```

## Tabulization:
```cpp
#include <bits/stdc++.h> 

int frogJump(int n, vector<int> &heights)
{
    vector<int> dp(n,0);
    dp[0] = 0;
    int fs,ss;
    for(int i=1;i<n;i++){
        fs= dp[i-1] + abs(heights[i]-heights[i-1]);
        ss = INT_MAX;
        if (i > 1)  ss = dp[i-2] + abs(heights[i]-heights[i-2]);

        dp[i] = min(fs,ss);
    }
    
    return dp[n-1];
}
```
