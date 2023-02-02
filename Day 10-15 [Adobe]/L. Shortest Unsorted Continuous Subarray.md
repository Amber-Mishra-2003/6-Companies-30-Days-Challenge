# Shortest Unsorted Continuous Subarray

Problem Link :- [Link](https://leetcode.com/problems/shortest-unsorted-continuous-subarray/)

<h3>
Problem :- Given an integer array nums, you need to find one continuous subarray that if you only sort this subarray in ascending order, then the whole array will be sorted in ascending order.

Return the shortest such subarray and output its length.

 
</h3>


**Solution :-**
```
class Solution {
public:
    int findUnsortedSubarray(vector<int>& nums) {
        
    stack<int> position;
    int start = INT_MAX;
    int end = INT_MAX;
    int highest = nums[0];
    position.push(0);
    for(int i=1; i<nums.size(); i++)
    {
        if(highest <= nums[i])
        {
            highest = nums[i];
            position.push(i);
        }
        else
        {
            end = i;
            int prev = -1;
            while(!position.empty())
            {
                if(nums[position.top()] > nums[i])
                {
                    prev = position.top();
                    position.pop();
                }
                else
                {
                    if(prev == -1)
                        break;
                    
                    nums[prev] = nums[i];
                    if(prev<=start)
                    {
                        start = prev;
                        position.push(prev);
                    }
                        
                    break;
                }
            }
            
            if(position.empty())
            {
                start = 0;
                nums[0] = nums[i];
                position.push(0);
            }
        }
    }
    
    if(start == INT_MAX)
        return 0;
    return (end - start + 1);
}
};
```
