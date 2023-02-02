# Factorial Trailing Zeroes

Problem Link :- [Link](https://leetcode.com/problems/factorial-trailing-zeroes/)

<h3>
Problem :- Given an integer n, return the number of trailing zeroes in n!.

Note that n! = n * (n - 1) * (n - 2) * ... * 3 * 2 * 1.
</h3>


**Solution :-**
```
class Solution {
public:
   int trailingZeroes(int n) 
   {
     
        int ans = 0;
        int div = 5;
        
        while(n/div != 0)
        {
            ans += n/div;
            div *= 5;
        }
        
        return ans;
    }
};
```
