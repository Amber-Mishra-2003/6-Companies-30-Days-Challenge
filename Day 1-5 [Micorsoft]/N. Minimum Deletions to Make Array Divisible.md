# Minimum Deletions to Make Array Divisible

Problem Link :- [Link](https://leetcode.com/problems/minimum-deletions-to-make-array-divisible/)

<h3>
Problem :-You are given two positive integer arrays nums and numsDivide. You can delete any number of elements from nums.
  
  
Return the minimum number of deletions such that the smallest element in nums divides all the elements of numsDivide. If this is not possible, return -1.

Note that an integer x divides y if y % x == 0.
  
  
</h3>


**Solution :-**

```
class Solution {
public:
    int minOperations(vector<int>& nums, vector<int>& numsDivide)
    {
        int gcd = numsDivide[0];
		
        for(int i=0;i<numsDivide.size();i++)
        {
            gcd = __gcd(gcd, numsDivide[i]);
        }
       
        sort(nums.begin(), nums.end());
		
        for(int i=0;i<nums.size();i++){
            if (gcd%nums[i] == 0){
                return i;
            }
        }
        
        return -1;
    }
};
```
