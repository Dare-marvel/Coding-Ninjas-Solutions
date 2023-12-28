### [Ninja’s Training](https://www.codingninjas.com/studio/problems/ninja-s-training_3621003)

## Explanation:

## Time and Space Complexity:
### `Time Complexity`:

### `Space Complexity`:

## Recursion( 2/5 Test cases passed):
```cpp
int helper(int day,int last,vector<vector<int>> &points){
    if(day == 0){
        int maxi=0;
        for(int task=0;task<3;task++){
            if(task!=last){
                maxi = max(maxi,points[0][task]);
            }
        }
        return maxi;
    }

    int maxi = 0;

    for(int task=0;task<3;task++){
            if(task!=last){
                int point= points[day][task] + helper(day-1,task,points);
                maxi = max(maxi,point);
            }
        }
    return maxi;

}
int ninjaTraining(int n, vector<vector<int>> &points)
{
     return helper(n-1, 3, points);
}
```

## Dynamic Programming:
```cpp
int helper(int day,int last,vector<vector<int>> &points,vector<vector<int>> &dp){
    if(day == 0){
        int maxi=0;
        for(int task=0;task<3;task++){
            if(task!=last){
                maxi = max(maxi,points[0][task]);
            }
        }
        return maxi;
    }

    if(dp[day][last] != -1) return dp[day][last];

    int maxi = 0;

    for(int task=0;task<3;task++){
            if(task!=last){
                int point= points[day][task] + helper(day-1,task,points,dp);
                maxi = max(maxi,point);
            }
        }
    return dp[day][last] = maxi;

}
int ninjaTraining(int n, vector<vector<int>> &points)
{
    vector<vector<int>> dp(n,vector<int>(4,-1));
    return helper(n-1, 3, points,dp);
}
```

## Tabulization:
```cpp

```
