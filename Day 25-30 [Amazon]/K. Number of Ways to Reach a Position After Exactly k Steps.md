# Number of Ways to Reach a Position After Exactly k Steps

Problem Link :- [Link](https://leetcode.com/problems/number-of-ways-to-reach-a-position-after-exactly-k-steps/)

<h3>
Problem :-You are given two positive integers startPos and endPos. Initially, you are standing at position startPos on an infinite number line. With one step, you can move either one position to the left, or one position to the right.

Given a positive integer k, return the number of different ways to reach the position endPos starting from startPos, such that you perform exactly k steps. Since the answer may be very large, return it modulo 109 + 7.

Two ways are considered different if the order of the steps made is not exactly the same.

Note that the number line includes negative integers.

  
</h3>


**Solution :-**
```
class Solution {
public:
    int fun(int st , int end , int k , int move , vector<vector<int>>&dp )
    {
        if(move >= k)
        {
            if(st == end) return 1 ;
            else  return 0 ;
        }
        if(dp[st+1000][move+1000] != -1)  return dp[st+1000][move+1000] % 1000000007 ;
        
        int l = fun(st-1 , end , k , move+1 , dp) ;
        int r = fun(st+1 , end , k , move+1 , dp) ;
        
        return dp[st+1000][move+1000] = (l % 1000000007 + r % 1000000007) % 1000000007 ;
    }
    
    int numberOfWays(int st , int end , int k) {
        
        vector<vector<int>> dp(3000 , vector<int>(3000 , -1)) ;
        return fun(st , end , k , 0 , dp) ;
        
    }
};
```
