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
class Solution {
    int findMaxPathSum(TreeNode* root, int& maxSum) {
        if (root == nullptr)
            return 0;
        int leftSum = findMaxPathSum(root->left, maxSum);
        int rightSum = findMaxPathSum(root->right, maxSum);
        int subTreeSum = std::max(leftSum, rightSum) + root->val;
        // consider current node as root and then check for max sum
        maxSum = std::max({maxSum, leftSum + rightSum + root->val, subTreeSum, root->val}); // update global max variable
        return std::max(subTreeSum, root->val);
    }
    
public:
    // Time: O(N), space: O(H) [H = tree height -> log N or N]
    int maxPathSum(TreeNode* root) {
        int maxSum = INT_MIN;
        return std::max(maxSum, findMaxPathSum(root, maxSum));
    }
};
```
- Time: `O(N)` since each node is visited only once.
- Space: `O(H)` where `H` is the height of the tree which is generally `log N`. In the worst case, the tree is a linked list, so the height is `N` so complexity becomes 