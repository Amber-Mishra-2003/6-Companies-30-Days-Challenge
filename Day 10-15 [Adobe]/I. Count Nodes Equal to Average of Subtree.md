# Count Nodes Equal to Average of Subtree

Problem Link :- [Link](https://leetcode.com/problems/count-nodes-equal-to-average-of-subtree/)

<h3>
Problem :- Given the root of a binary tree, return the number of nodes where the value of the node is equal to the average of the values in its subtree.

Note:

  * The average of n elements is the sum of the n elements divided by n and rounded down to the nearest integer.
  
  * A subtree of root is a tree consisting of root and all of its descendants.
 
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
    
    void Sum_and_nodecount(TreeNode* root,int &sum,int &nodecount){
        if(root){
            sum+=root->val;
            nodecount++;
            Sum_and_nodecount(root->left,sum,nodecount);
            Sum_and_nodecount(root->right,sum,nodecount);
        }
    }
    void Count_Node(TreeNode* root,int &ans){
        if(root==NULL)return;
        int nodecount=0,sum=0;
        Sum_and_nodecount(root,sum,nodecount);
        if((sum/nodecount)==root->val){
            ans++;
        }
        Count_Node(root->left,ans);
        Count_Node(root->right,ans);
    }
    int averageOfSubtree(TreeNode* root) {
        int ans=0;
        Count_Node(root,ans);
        return ans;
    }
};
```
