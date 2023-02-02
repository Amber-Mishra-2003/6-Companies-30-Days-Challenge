# Combination Sum III

Problem Link :- [Link](https://leetcode.com/problems/combination-sum-iii/)

<h3>
Problem : -
Find all valid combinations of k numbers that sum up to n such that the following conditions are true:
  
    1.  Only numbers 1 through 9 are used.
    2.  Each number is used at most once.
  
Return a list of all possible valid combinations. The list must not contain the same combination twice, and the combinations may be returned in any order.
</h3>



**Solution : -**
```
class Solution {
public:
       void helper(vector<vector<int>>& output, int k, int n, int num,  vector<int> currentGroup)     
       {
        if(n ==0 && k ==0)
        {
            output.push_back(currentGroup);
            return;
        }
        
        if(num <= 0) return;
        
        if(num <= n)
        {
            currentGroup.push_back(num);
            helper(output, k-1, n-num, num-1, currentGroup);
            currentGroup.pop_back();      
        }
		
        helper(output, k, n, num-1, currentGroup);
    }
    
    vector<vector<int>> combinationSum3(int k, int n) 
    {
        vector<vector<int>> output;
        vector<int> currGroup;
        int num = 9;
        helper(output, k , n, num,  currGroup);
        return output;
    }
};
```
