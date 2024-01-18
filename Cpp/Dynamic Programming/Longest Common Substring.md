### [Longest Common Substring](https://www.codingninjas.com/studio/problems/longest-common-substring_1235207?source=youtube&campaign=striver_dp_videos&utm_source=youtube&utm_medium=affiliate&utm_campaign=striver_dp_videos&leftPanelTabValue=PROBLEM)

## Explanation:
1. **Function Declaration**: The function `lcs` is declared with two parameters, `str1` and `str2`, which are references to `std::string` objects. This function returns an `int`.

2. **Variable Initialization**: The variables `n` and `m` are initialized with the sizes of `str1` and `str2` respectively. These represent the lengths of the two input strings.

3. **Dynamic Programming Table**: A 2D `std::vector` named `dp` is created. The dimensions of this vector are `(n+1)` by `(m+1)`, and it's initially filled with zeros. This table will be used to store the lengths of the longest common substrings found so far.

4. **Table Initialization**: The first row and the first column of the `dp` table are filled with zeros. This represents the case where one of the strings is empty.

5. **Main Logic**: The main logic of the function is contained within two nested `for` loops that iterate over the `dp` table. For each cell `dp[ind1][ind2]`, it checks if the characters at positions `ind1-1` in `str1` and `ind2-1` in `str2` are the same. If they are, it sets `dp[ind1][ind2]` to `1 + dp[ind1-1][ind2-1]`, which means it extends the longest common substring found so far. If they are not the same, it sets `dp[ind1][ind2]` to `0`, which means the longest common substring ends here.

6. **Result Calculation**: The variable `ans` is used to keep track of the length of the longest common substring found so far. It's updated whenever a longer common substring is found.

7. **Return Statement**: Finally, the function returns `ans`, which is the length of the longest common substring of `str1` and `str2`.

## Time and Space Complexity:
### `Time Complexity`:
The time complexity of this code is **O(n*m)**, where `n` and `m` are the lengths of the input strings. This is because each cell in the `dp` table is filled exactly once.

### `Space Complexity`:
The space complexity of this code is also **O(n*m)**, due to the space required for the `dp` table.

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
