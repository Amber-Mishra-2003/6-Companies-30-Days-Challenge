# House Robber III

Problem Link :- [Link](https://leetcode.com/problems/house-robber-iii/)

<h3>
Problem :- The thief has found himself a new place for his thievery again. There is only one entrance to this area, called root.

Besides the root, each house has one and only one parent house. After a tour, the smart thief realized that all houses in this place form a binary tree. It will automatically contact the police if two directly-linked houses were broken into on the same night.

Given the root of the binary tree, return the maximum amount of money the thief can rob without alerting the police.
</h3>


**Solution :-**
```
struct Rob
{
    int withRobbery;
    int withoutRobbery;
    Rob(){
        withRobbery=0;
        withoutRobbery=0;
    }
};
class Solution {
public:   
int rob(TreeNode* root) {
        Rob result=fun(root);
    return max(result.withRobbery,result.withoutRobbery); 
    }
    Rob fun(TreeNode* root)
    {
      if(!root)
          return Rob();
        
       
        Rob left=fun(root->left);
        
   
        Rob right=fun(root->right);
        
       
      Rob ans=Rob();
        ans.withRobbery=root->val;
        ans.withRobbery+=(left.withoutRobbery+right.withoutRobbery);
        
       
           ans.withoutRobbery=0;
          ans.withoutRobbery+=max(left.withoutRobbery,left.withRobbery)+max(right.withoutRobbery,right.withRobbery);
        return ans;
     
    }
};
```
