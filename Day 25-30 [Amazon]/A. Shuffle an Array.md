# Shuffle an Array

Problem Link :- [Link](https://leetcode.com/problems/shuffle-an-array/)

<h3>
Problem :- Given an integer array nums, design an algorithm to randomly shuffle the array. All permutations of the array should be equally likely as a result of the shuffling.

Implement the Solution class:

  * Solution(int[] nums) Initializes the object with the integer array nums.
  
  * int[] reset() Resets the array to its original configuration and returns it.
  
  * int[] shuffle() Returns a random shuffling of the array.
</h3>


**Solution :-**
```
class Solution {
vector<int> original;
	int n;
public:

	Solution(vector<int>& nums) {
		original = nums;
		n = original.size();
	}
	
	vector<int> reset() {
		return original;
	}
	
	vector<int> shuffle() {
			vector<int> shuffled = original;
			
			int leftSize = n;
			for(int i = n-1; i>=0; i--) {
				int j = rand()%leftSize;
				swap(shuffled[i], shuffled[j]);
				leftSize--;
			}
			return shuffled;
	}
	
};
```
