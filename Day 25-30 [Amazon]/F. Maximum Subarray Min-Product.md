# Maximum Subarray Min-Product

Problem Link :- [Link](https://leetcode.com/problems/maximum-subarray-min-product/)

<h3>
Problem :- The min-product of an array is equal to the minimum value in the array multiplied by the array's sum.

  * For example, the array [3,2,5] (minimum value is 2) has a min-product of 2 * (3+2+5) = 2 * 10 = 20.
  
  
Given an array of integers nums, return the maximum min-product of any non-empty subarray of nums. Since the answer may be large, return it modulo 109 + 7.

Note that the min-product should be maximized before performing the modulo operation. Testcases are generated such that the maximum min-product without modulo will fit in a 64-bit signed integer.

A subarray is a contiguous part of an array.
</h3>


**Solution :-**
```
class Solution {
public:
    int maxSumMinProduct(vector<int>& nums) {
        long mod = 1e9 + 7;
		long res = 0;
		nums.push_back(-1);
		int length = nums.size();
		stack<int> st;
		vector<long> dp(length);
		dp[0] = nums[0];
		for (int i = 1; i < length-1; i++) { 
			dp[i] = dp[i - 1] + nums[i]; 
		}
		for (int i = 0; i < length; i++) {
			while (!st.empty() && nums[i] < nums[st.top()]) {
				int top = st.top();
				st.pop();

				if (!st.empty()) {
					long x = dp[i - 1] - dp[st.top()];
					//cout << x<<endl;
					res = (x * nums[top]) > res ? (x * nums[top]) : res;
				}
				else {
					long x = dp[i-1];
					res = (x * nums[top]) > res ? (x * nums[top]) : res;
				}
			}
			st.push(i);
		}
		return res % mod;
    }
};
```
