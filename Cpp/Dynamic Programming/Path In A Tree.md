### [Path In A Tree](https://www.codingninjas.com/studio/problems/path-in-a-tree_3843990?leftPanelTabValue=PROBLEM)

## Explanation:
Sure, let's break down the code:

1. **Template Class TreeNode**: This is a template class for a binary tree node. Each node has a data member of type `T` (defaulted to `int`), and two pointers (`left` and `right`) pointing to its left child and right child respectively. There are two methods in this class:
    - **Constructor**: This method is used to create a new node with the given data. The `left` and `right` pointers are initialized to `NULL`.
    - **Destructor**: This method is used to delete the node. If the `left` and `right` children are not `NULL`, they are deleted to free up memory.

2. **Function getPath**: This is a helper function that finds the path from the root to a node with a given value `x`. It takes three arguments: a pointer to the root of the tree, a reference to a vector `arr` to store the path, and the value `x`. The function works as follows:
    - If the root is `NULL`, it returns `false` because a `NULL` tree does not contain `x`.
    - It adds the data of the root to `arr`.
    - If the data of the root is `x`, it returns `true` because it has found `x`.
    - If `x` is not found in the root, it recursively checks the left and right subtrees. If `x` is found in either subtree, it returns `true`.
    - If `x` is not found in either subtree, it removes the data of the root from `arr` and returns `false`.

3. **Function pathInATree**: This function finds the path from the root to a node with a given value `x` in a binary tree. It takes two arguments: a pointer to the root of the tree and the value `x`. The function works as follows:
    - It creates an empty vector `arr` to store the path.
    - If the root is `NULL`, it returns `arr` because a `NULL` tree does not contain `x`.
    - It calls the helper function `getPath` with the root, `arr`, and `x`. After the call, `arr` contains the path from the root to `x`.
    - It returns `arr`.

## Time and Space Complexity:
### `Time Complexity`:
The **time complexity** of the code is **O(n)**, where **n** is the number of nodes in the tree. This is because in the worst case, the function `getPath` may need to visit all nodes in the tree.

### `Space Complexity`:
The **space complexity** of the code is **O(h)**, where **h** is the height of the tree. This is due to the recursive stack used by the `getPath` function and the space used by the vector `arr` to store the path. In the worst case, the height of the tree is **n** (for a skewed tree), so the space complexity is **O(n)**.

## Code:
```cpp
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */

// Definition of a class named Solution
class Solution {
public:
    // Helper function to check if two subtrees are symmetric
    bool isSymmetricHelp(TreeNode* left, TreeNode* right) {
        // Base case: If either subtree is NULL, they are symmetric if both are NULL
        if (left == NULL || right == NULL) {
            return left == right;
        }

        // Check if values of the current nodes are equal
        if (left->val != right->val) {
            return false;
        }

        // Recursively check the symmetry of the left and right subtrees
        return isSymmetricHelp(left->left, right->right) && isSymmetricHelp(left->right, right->left);
    }

    // Main function to check if a binary tree is symmetric
    bool isSymmetric(TreeNode* root) {
        // The tree is considered symmetric if it is empty or if its left and right subtrees are symmetric
        return root == NULL || isSymmetricHelp(root->left, root->right);
    }
};
```
