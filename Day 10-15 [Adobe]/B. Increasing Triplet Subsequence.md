# Increasing Triplet Subsequence

Problem Link :- [Link](https://leetcode.com/problems/increasing-triplet-subsequence/description/)

<h3>
Problem :- Given an integer array nums, return true if there exists a triple of indices (i, j, k) such that i < j < k and nums[i] < nums[j] < nums[k]. If no such indices exists, return false.
</h3>


**Solution :-**
```
class Solution {
public:
    bool increasingTriplet(vector<int>& nums) {
        if (nums.size()<=2) return false;
        
        int low = INT_MAX, mid = INT_MAX;

        for (int i=0; i<nums.size(); i++) {

            if (nums[i] > mid) return true;

            else if (nums[i]>low && nums[i]<mid) mid = nums[i];

            else if (nums[i] < low) low = nums[i];
        }
    
    return false;
    }
};
```
