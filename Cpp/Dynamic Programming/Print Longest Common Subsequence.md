### [Print Longest Common Subsequence](https://www.codingninjas.com/studio/problems/print-longest-common-subsequence_8416383?leftPanelTabValue=PROBLEM)

## Explanation:
This code is an implementation of the **Longest Common Subsequence (LCS)** problem using **dynamic programming**. Here's a detailed explanation of the code:

1. **Function Signature**: The function `findLCS` takes four parameters: two integers `n` and `m` representing the lengths of two strings `s1` and `s2`, and the two strings `s1` and `s2`.

2. **Dynamic Programming Table**: A 2D vector `dp` of size `(n+1)x(m+1)` is initialized with all elements as `0`. This table will store the length of the LCS for all prefixes of `s1` and `s2`.

3. **Table Initialization**: The first row and the first column of the table are initialized to `0` as the LCS of any string with an empty string is an empty string.

4. **Table Filling**: The table is filled in a row-wise manner. For each cell `dp[i][j]`, if the `i-th` character of `s1` is equal to the `j-th` character of `s2`, `dp[i][j]` is set to `1 + dp[i-1][j-1]`. If they are not equal, `dp[i][j]` is set to the maximum of `dp[i][j-1]` and `dp[i-1][j]`.

5. **Length of LCS**: After filling the table, `dp[n][m]` will contain the length of the LCS of `s1` and `s2`.

6. **Reconstruction of LCS**: The LCS is reconstructed from the `dp` table. An empty string `ans` of length `len` is initialized with all characters as `$`. Starting from `dp[n][m]`, if `s1[i-1]` is equal to `s2[j-1]`, the character is added to `ans` at the `index` position and `index`, `i`, and `j` are decremented. If `s1[i-1]` is not equal to `s2[j-1]`, the direction of movement is decided based on which of `dp[i-1][j]` or `dp[i][j-1]` is greater.

7. **Return Value**: The function returns the string `ans` which is the LCS of `s1` and `s2`.

Please note that the indices in C++ are 0-based, so `s1[i-1]` and `s2[j-1]` are used instead of `s1[i]` and `s2[j]`. Also, the dynamic programming table `dp` is of size `(n+1)x(m+1)` to handle the case when the entire strings `s1` and `s2` are considered. The extra row and column (initialized to `0`) handle the base case when one of the strings is empty. I hope this explanation helps! 😊
## Time and Space Complexity:
### `Time Complexity`:
The **time complexity** of this code is **O(n*m)** because there are two nested loops running `n` and `m` times.

### `Space Complexity`:
The **space complexity** is also **O(n*m)** due to the `dp` table. The code is efficient and suitable for large inputs of `n` and `m`.

## Code:
```cpp
// Function to find the Longest Common Subsequence (LCS) of two strings
string findLCS(int n, int m, string &s1, string &s2) {
    // Create a 2D vector to store the lengths of LCS for different substrings
    vector<vector<int>> dp(n + 1, vector<int>(m + 1, 0));

    // Populate the dp matrix using dynamic programming
    for (int i = 0; i <= n; i++) {
        for (int j = 0; j <= m; j++) {
            // Base case: if either string is empty, LCS is 0
            if (i == 0 || j == 0) {
                dp[i][j] = 0;
            }
            // If characters match, extend the LCS by 1
            else if (s1[i - 1] == s2[j - 1])
                dp[i][j] = 1 + dp[i - 1][j - 1];
            // If characters don't match, take the maximum LCS from the previous row or column
            else
                dp[i][j] = max(dp[i][j - 1], dp[i - 1][j]);
        }
    }

    // Retrieve the length of LCS from the bottom-right cell of the matrix
    int len = dp[n][m];
    int index = len - 1;
    // Initialize a string to store the LCS
    string ans = "";

    // Initialize pointers for string traversal
    int i = n, j = m;

    // Fill the LCS string by backtracking through the dp matrix
    for (int k = 0; k < len; k++) ans += '$';

    while (i > 0 && j > 0) {
        if (s1[i - 1] == s2[j - 1]) {
            ans[index] = s1[i - 1];
            index--;
            i--, j--;
        } else if (dp[i - 1][j] > dp[i][j - 1]) {
            i--;
        } else {
            j--;
        }
    }

    // Return the LCS string
    return ans;
}

```
