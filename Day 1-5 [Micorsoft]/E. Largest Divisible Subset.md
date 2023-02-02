# Largest Divisible Subset

Problem Link : - [Link](https://leetcode.com/problems/largest-divisible-subset/)

<h3>
Problem : - Given a set of distinct positive integers nums, return the largest subset answer such that every pair (answer[i], answer[j]) of elements in this subset satisfies:

* answer[i] % answer[j] == 0, or
* answer[j] % answer[i] == 0
  
  
If there are multiple solutions, return any of them.
  
</h3>



**Solution : -**

```
class Solution {
public:
    vector<int> largestDivisibleSubset(vector<int>& nums) {
        vector<int> LIS[nums.size()];
        if(nums.size()==0){
            vector<int> v;
            return v;
        }
        sort(nums.begin(),nums.end());
        LIS[0].push_back(nums[0]);
        for(int i=1;i<nums.size();i++){
            for(int j=0;j<i;j++){
                if(nums[i]>nums[j] && LIS[j].size()>LIS[i].size() && (nums[j]%nums[i]==0 || nums[i]%nums[j]==0)){
                    LIS[i]=LIS[j];
                }
            }
            LIS[i].push_back(nums[i]);
        }
        int j=0;
        for(int i=0;i<nums.size();i++){
            if(LIS[j].size()<LIS[i].size()){
                j=i;
            }
        }
        return LIS[j];
        
    }
};

```

