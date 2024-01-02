### [Subset Sum Equal To K]()

## Explanation:

## Time and Space Complexity:
### `Time Complexity`:

### `Space Complexity`:

## Tabulization:
```cpp

```

## Recursion:
```cpp
#include <bits/stdc++.h> 

bool subsetUtil(int ind,int target,vector<int> &arr) {
    if (target == 0 ) return true;

    if ( ind == 0 ) return arr[ind] == target;

    bool notTake = subsetUtil(ind-1,target,arr);
    bool take = false;

    if(target >= arr[ind]) {
        take = subsetUtil(ind-1, target-arr[ind], arr);
    }

    return take || notTake;
}
bool subsetSumToK(int n, int k, vector<int> &arr) {
    // Write your code here.
    return subsetUtil(n,k,arr);
}
```
