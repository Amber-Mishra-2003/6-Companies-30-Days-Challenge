# Count Nice Pairs in an Array

Problem Link :- [Link](https://leetcode.com/problems/count-nice-pairs-in-an-array/)

<h3>
Problem :- You are given an array nums that consists of non-negative integers. Let us define rev(x) as the reverse of the non-negative integer x. For example, rev(123) = 321, and rev(120) = 21. A pair of indices (i, j) is nice if it satisfies all of the following conditions:

    * 0 <= i < j < nums.length
    * nums[i] + rev(nums[j]) == nums[j] + rev(nums[i])
Return the number of nice pairs of indices. Since that number can be too large, return it modulo 109 + 7.
</h3>



**Solution :-**
```
class Solution {
public:
    int mod=1000000007;
    int rev(int n) {
        int s=0;
        while(n) {
            s=s*10+n%10;
            n/=10;
        }
        return s;
    }
    int countNicePairs(vector<int>& nums) {
        int cnt=0;
        unordered_map<int,int> mp;
        for(int i=0; i<nums.size(); i++) cnt=(cnt+mp[nums[i]-rev(nums[i])]++)%mod;
        return cnt;
    }
};
```
