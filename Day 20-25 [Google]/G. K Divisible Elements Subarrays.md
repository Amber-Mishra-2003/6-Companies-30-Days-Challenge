# K Divisible Elements Subarrays

Problem Link :- [Link](https://leetcode.com/problems/k-divisible-elements-subarrays/)

<h3>
Problem :- Given an integer array nums and two integers k and p, return the number of distinct subarrays which have at most k elements divisible by p.

Two arrays nums1 and nums2 are said to be distinct if:

  * They are of different lengths, or
  
  * There exists at least one index i where nums1[i] != nums2[i].
  
A subarray is defined as a non-empty contiguous sequence of elements in an array.
</h3>


**Solution :-**
```
class Solution {
public:
    int countDistinct(vector<int>& nums, int k, int p) {
        int n = nums.size();
        vector<int> dp (n, 0);
        set<vector<int>> res;
        vector<vector<int>> uniques(n);
        dp[0] = nums[0] % p == 0;
        for(int i = 1; i < n; i++)
            dp[i] = dp[i - 1] + (nums[i] % p == 0);
        int count = 0;
        for(int i = 0; i < n; i++)
            for(int j = i; j < n; j++) {
                int Divisible_count = i > 0 ? (dp[j] - dp[i-1]) : dp[j];
                if(Divisible_count > k)     break;
                count += isunique(i, j, nums, uniques);
            }
        return count;
    }
    
    bool isunique (int s, int e, vector<int>& nums, vector<vector<int>>& uniques) {
        int size = e - s;
        for(int i = 0; i < uniques[size].size(); i++) {
            bool the_same = true;
            int prev_s = uniques[size][i];
            for(int j = s; j <= e; j++) 
                if(nums[j] != nums[prev_s + j - s]) {
                    the_same = false;
                    break;
                }
            if(the_same)    return false;
        }
        uniques[size].push_back(s);
        return true;
    }
};
```
