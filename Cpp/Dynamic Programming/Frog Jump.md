### [Frog Jump](https://www.codingninjas.com/studio/problems/frog-jump_3621012)

## Explanation (Recursion):
This C++ code is a solution to the problem of finding the minimum total cost for a frog to reach the top of a set of heights, where the frog can either jump one or two steps at a time, and the cost of each jump is the absolute difference in heights. Here's a detailed explanation:

1. **Including Libraries**: The code begins with `#include <bits/stdc++.h>`, which is a header file in C++ that includes most standard library files.

2. **Helper Function**: A helper function named `helper` is defined, which takes an index `ind` and a reference to a vector of integers `heights`. This function is used to calculate the minimum cost for the frog to reach the height at index `ind`.

3. **Base Case**: If `ind` is 0, the function returns 0. This is because if the frog is already at the first height, no jumps are needed, so the cost is 0.

4. **Recursive Case**: If `ind` is not 0, the function calculates two possible costs: `left` and `right`. `left` is the cost of jumping from the previous height, which is the cost of reaching the previous height plus the absolute difference in heights. `right` is the cost of jumping from the height before the previous height, which is the cost of reaching that height plus the absolute difference in heights. However, `right` is only calculated if `ind` is greater than 1, because the frog can't jump two steps from the first height.

5. **Minimum Cost**: The function returns the minimum of `left` and `right`, which is the minimum cost for the frog to reach the height at index `ind`.

6. **frogJump Function**: The `frogJump` function is defined, which takes an integer `n` and a reference to a vector of integers `heights`, and returns an integer. This function simply calls the `helper` function with `n-1` as the index, and returns the result. This is because the frog wants to reach the top, which is the last height in `heights`, and since indexing is 0-based, the index of the last height is `n-1`.

## Time and Space Complexity:
### `Time Complexity`:
The time complexity of the code is **O(2^n)**, because in the worst case, the `helper` function makes two recursive calls in each call.

### `Space Complexity`:
The space complexity is **O(n)**, because in the worst case, the maximum depth of the recursion tree is `n`, which is the maximum amount of space needed on the call stack.

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
