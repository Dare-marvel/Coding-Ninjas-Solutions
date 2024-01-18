### [Longest Common Substring](https://www.codingninjas.com/studio/problems/longest-common-substring_1235207?source=youtube&campaign=striver_dp_videos&utm_source=youtube&utm_medium=affiliate&utm_campaign=striver_dp_videos&leftPanelTabValue=PROBLEM)

## Explanation:

## Time and Space Complexity:
### `Time Complexity`:

### `Space Complexity`:

## Code:
```cpp
#include <iostream>
#include <vector>
#include <string>

// Function to calculate the length of the Longest Common Subsequence (LCS)
int lcs(std::string &str1, std::string &str2) {
    // Get the lengths of input strings
    int n = str1.size();
    int m = str2.size();

    // Initialize a 2D vector for dynamic programming
    std::vector<std::vector<int>> dp(n + 1, std::vector<int>(m + 1, 0));

    // Initialize base cases: when one of the strings is empty
    for (int i = 0; i <= n; i++) {
        dp[i][0] = 0;
    }
    for (int i = 0; i <= m; i++) {
        dp[0][i] = 0;
    }

    // Variable to store the length of the Longest Common Subsequence
    int ans = 0;

    // Iterate over the characters of both strings
    for (int ind1 = 1; ind1 <= n; ind1++) {
        for (int ind2 = 1; ind2 <= m; ind2++) {
            // Check if the characters match
            if (str1[ind1 - 1] == str2[ind2 - 1]) {
                // If there is a match, update the LCS length
                dp[ind1][ind2] = 1 + dp[ind1 - 1][ind2 - 1];
                ans = std::max(ans, dp[ind1][ind2]);
            } else {
                // If characters don't match, reset the length to 0
                dp[ind1][ind2] = 0;
            }
        }
    }

    // Return the length of the Longest Common Subsequence
    return ans;
}
```
