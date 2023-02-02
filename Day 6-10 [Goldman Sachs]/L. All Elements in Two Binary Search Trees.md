# All Elements in Two Binary Search Trees

Problem Link :- [Link](https://leetcode.com/problems/all-elements-in-two-binary-search-trees/)

<h3>
Problem :-Given two binary search trees root1 and root2, return a list containing all the integers from both trees sorted in ascending order. 
</h3>


**Solution :-**
```
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
public:
    void inorder(TreeNode* root, vector<int>&ans)
    {
        if(root == NULL)
        {
            return;
        }
        inorder(root->left,ans);
        ans.push_back(root->val);
        inorder(root->right,ans);
        return;
    }
    vector<int> getAllElements(TreeNode* root1, TreeNode* root2) 
    {
        vector<int>ans;

        inorder(root1,ans);
        inorder(root2,ans);

        sort(ans.begin(),ans.end());
        return ans;

    }
};
```
