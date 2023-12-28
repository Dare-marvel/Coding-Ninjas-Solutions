### []()

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

```
