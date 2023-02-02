# Partition to K Equal Sum Subsets

Problem Link :- [Link](https://leetcode.com/problems/partition-to-k-equal-sum-subsets/)

<h3>
Problem : - Given an integer array nums and an integer k, return true if it is possible to divide this array into k non-empty subsets whose sums are all equal.
</h3>


**Solution :-**
```
class Solution {
public:
    bool canPartitionKSubsets(vector<int>& nums, int k) {
        sort(begin(nums), end(nums), greater<int>());
        int sum = accumulate(begin(nums), end(nums), 0);
        if (sum % k != 0) {
            return false;
        }
        vector<bool> used(size(nums));
        return backtrack(nums, sum / k, k, 0, 0, used);
    }
private:
    bool backtrack(vector<int>& nums, int target, int k, int bucket, int start, vector<bool>& used) {
        if (k == 1) {
            return true;
        }
        
        if (bucket > target || start >= size(nums)) {
            return false;
        }
        
        if (bucket == target) {
            return backtrack(nums, target, k - 1, 0, 0, used);
        }
        
        for (int i = start; i < size(nums); ++i) {
            if (used[i]) {
                continue;
            }
            used[i] = true;
            if (backtrack(nums, target, k, bucket + nums[i], i + 1, used)) {
                return true;
            }
            used[i] = false;
        }
        
        return false;
    }
};
```
