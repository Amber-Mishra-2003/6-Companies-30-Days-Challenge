# Rotate Function

Problem Link :- [Link](https://leetcode.com/problems/rotate-function/)

<h3>
Problem:- You are given an integer array nums of length n.Assume arrk to be an array obtained by rotating nums by k positions clock-wise. We define the rotation function F on nums as follow:

  
  
  
****  F(k) = 0 * arrk[0] + 1 * arrk[1] + ... + (n - 1) * arrk[n - 1].
  
  
Return the maximum value of F(0), F(1), ..., F(n-1).The test cases are generated so that the answer fits in a 32-bit integer.
  </h3>




**Solution : -**

```
class Solution 
{
public:
    int maxRotateFunction(vector<int>& A) 
    {
        if (A.size() == 0) return 0;
        int sum = 0, current = 0;
        for(int i = 0; i < A.size(); ++i)
        {
            sum+= A[i];
            current+= i * A[i];
        }
        int maximum = INT_MIN;
        for (int i = A.size() - 1; i >=0; --i) 
        {
            current+= sum - A.size() * A[i];
            maximum = max(maximum, current);
        }
        return maximum;
    }
};
```
