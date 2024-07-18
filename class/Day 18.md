## Flatten Binary Tree to Linked List
With post order
```cpp
class Solution {
public:
    void flatten(TreeNode* root) {
        TreeNode* prev = nullptr;
        flattenHelper(root, prev);
    }
private:
    void flattenHelper(TreeNode* node, TreeNode*& prev) {
        if (!node) return;

        flattenHelper(node->right, prev);
        flattenHelper(node->left, prev);

        node->right = prev;
        node->left = nullptr;
        prev = node;
    }
};
```
with pre order
```cpp
class Solution {
public:
    void flatten(TreeNode* root) {
        TreeNode* prev = nullptr;
        flattenHelper(root, root);
    }
private:
    void flattenHelper(TreeNode* root, TreeNode*& prev) {
        if (!root) return;
  
        TreeNode *left = prev->left;
        TreeNode *right = prev->right;

        if(root!=prev){
            prev->right = root;
            prev->left = NULL;
            prev = root;
        }

        flattenHelper(left, prev);
        flattenHelper(right, prev);
    }
};
```
## Maximum Width Of Binary Tree

## Binary Tree Maximum Path Sum
same as diameter but instead of taking edges we take nodes and for negative values we compare them with 0 and take 0 instead of taking them.
```cpp
class Solution {
int solve(TreeNode* root, int& maxi) {
    if (root == NULL)
        return 0;

    int lh = max(0, solve(root->left, maxi));
    int rh = max(0, solve(root->right, maxi));

    maxi = max(maxi, root->val + lh + rh);

    return root->val + max(lh, rh);
}
public:
    int maxPathSum(TreeNode* root) {
        int ans = INT_MIN;
        solve(root, ans);
        return ans;
    }
};
```


