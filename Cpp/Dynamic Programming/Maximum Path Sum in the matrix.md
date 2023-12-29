### [Maximum Path Sum in the matrix](https://www.codingninjas.com/studio/problems/maximum-path-sum-in-the-matrix_797998?source=youtube&campaign=striver_dp_videos&utm_source=youtube&utm_medium=affiliate&utm_campaign=striver_dp_videos)

## Explanation:

## Time and Space Complexity:
### `Time Complexity`:

### `Space Complexity`:

## Recursion:
```cpp
#include <bits/stdc++.h> 

int maxPaths(int i,int j,vector<vector<int>> &matrix){

    if(j<0 || j>=matrix[0].size()) return -1e8;

    if(i == 0) return matrix[0][j];


    int s = matrix[i][j] + maxPaths(i-1,j,matrix);
    int ld = matrix[i][j] + maxPaths(i-1, j-1, matrix);
    int rd = matrix[i][j] + maxPaths(i-1, j+1, matrix);

    return max(s,max(ld,rd)); 
}
int getMaxPathSum(vector<vector<int>> &matrix)
{
    int maximum = -1e8;
    for(int j=0;j<matrix[0].size();j++){
        maximum = max(maximum,maxPaths(matrix.size()-1,j,matrix));
    }

    return maximum;
}
```

## Memoization:
```cpp
#include <bits/stdc++.h> 

int maxPaths(int i,int j,vector<vector<int>> &matrix,vector<vector<int>> &dp){

    if(j<0 || j>=matrix[0].size()) return -1e8;

    if(i == 0) return matrix[0][j];

    if(dp[i][j] != -1) return dp[i][j];

    int s = matrix[i][j] + maxPaths(i-1,j,matrix,dp);
    int ld = matrix[i][j] + maxPaths(i-1, j-1, matrix,dp);
    int rd = matrix[i][j] + maxPaths(i-1, j+1, matrix,dp);

    return dp[i][j] = max(s,max(ld,rd)); 
}
int getMaxPathSum(vector<vector<int>> &matrix)
{
    int n = matrix.size();
    int m = matrix[0].size();
    vector<vector<int>> dp(n,vector<int>(m,-1));

    int maximum = -1e8;
    for(int j=0;j<m;j++){
        maximum = max(maximum,maxPaths(n-1,j,matrix,dp));
    }

    return maximum;
}
```

## Tabulization:
```cpp

```
