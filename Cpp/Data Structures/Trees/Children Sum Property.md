### [Children Sum Property](https://www.codingninjas.com/studio/problems/childrensumproperty_790723?leftPanelTabValue=PROBLEM)

## Explanation:
Sure, let's break down the code:

1. **Class BinaryTreeNode**: This is a template class for a binary tree node. Each node has a data member of type `T`, and two pointers (`left` and `right`) pointing to its left child and right child respectively. There is a constructor for creating a new node with a given data.

2. **Function changeTree**: This function modifies a binary tree in place. It takes a pointer to the root of the tree as an argument. The function works as follows:
    - If the root is `NULL`, it returns immediately because a `NULL` tree cannot be modified.
    - It calculates the sum of the data of the left child and the right child of the root (`child`).
    - If `child` is greater than or equal to the data of the root, it updates the data of the root to `child`. This is because the data of each node should be at least the sum of the data of its children.
    - If `child` is less than the data of the root, it updates the data of the left child or the right child to the data of the root. This is because the data of each node should be no more than the data of its parent.
    - It recursively calls `changeTree` on the left child and the right child of the root to modify the rest of the tree.
    - After modifying the children of the root, it updates the data of the root to the sum of the data of its children (`tot`). This is to ensure that the data of each node is the sum of the data of its children.

## Time and Space Complexity:
### `Time Complexity`:
The **time complexity** of the code is **O(n)**, where **n** is the number of nodes in the tree. This is because each node in the tree is visited once by the function `changeTree`.

### `Space Complexity`:
The **space complexity** of the code is **O(h)**, where **h** is the height of the tree. This is due to the recursive stack used by the function `changeTree`. In the worst case, the height of the tree is **n** (for a skewed tree), so the space complexity is **O(n)**.

## Code:
```cpp
#include <bits/stdc++.h> 

/*************************************************************

    Following is the Binary Tree node structure

    class BinaryTreeNode
    {
    public :
        T data;
        BinaryTreeNode < T > *left;
        BinaryTreeNode < T > *right;

        BinaryTreeNode(T data) {
            this -> data = data;
            left = NULL;
            right = NULL;
        }
    };

*************************************************************/

// Function to change the values of a binary tree node based on the sum of its children
void changeTree(BinaryTreeNode < int > * root) {
    // Base case: If the current node is NULL, return
    if(root == NULL) return;

    // Calculate the sum of children's data
    int child = 0;

    if(root->left) child += root->left->data;
    if(root->right) child += root->right->data;

    // Compare the sum with the current node's data
    if(child >= root->data) 
        root->data = child;
    else {
        // If the current node's data is greater, update the children's data accordingly
        if(root->left) root->left->data = root->data;
        else if(root->right) root->right->data = root->data;
    }

    // Recursively apply the same process to left and right subtrees
    changeTree(root->left);
    changeTree(root->right);

    // Recalculate the total sum of data in children
    int tot = 0;
    if(root->left) tot += root->left->data;
    if(root->right) tot += root->right->data;
    
    // Update the current node's data with the total sum
    if(root->left || root->right) 
        root->data = tot;
}  

```
