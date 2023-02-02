# Maximum Points in an Archery Competition

Problem Link :- [Link](https://leetcode.com/problems/maximum-points-in-an-archery-competition/)

<h3>
Problem :- Alice and Bob are opponents in an archery competition. The competition has set the following rules:

Alice first shoots numArrows arrows and then Bob shoots numArrows arrows.
  
The points are then calculated as follows:
  
The target has integer scoring sections ranging from 0 to 11 inclusive.
  
For each section of the target with score k (in between 0 to 11), say Alice and Bob have shot ak and bk arrows on that section respectively. If ak >= bk, then Alice takes k points. If ak < bk, then Bob takes k points.

However, if ak == bk == 0, then nobody takes k points.

   * For example, if Alice and Bob both shot 2 arrows on the section with score 11, then Alice takes 11 points. On the other hand, if Alice shot 0 arrows on the section with score 11 and Bob shot 2 arrows on that same section, then Bob takes 11 points.

You are given the integer numArrows and an integer array aliceArrows of size 12, which represents the number of arrows Alice shot on each scoring section from 0 to 11. Now, Bob wants to maximize the total number of points he can obtain.

Return the array bobArrows which represents the number of arrows Bob shot on each scoring section from 0 to 11. The sum of the values in bobArrows should equal numArrows.

If there are multiple ways for Bob to earn the maximum total points, return any one of them.

 
</h3>


**Solution :-**
```
class Solution {
     int dp[100001][13];
public:
    int helper(int numArrows, vector<int>& aliceArrows, int n) 
    {
        if(numArrows == 0) return 0;
        if(n == 0) return 0;
        if(dp[numArrows][n] != -1) return dp[numArrows][n];
        
        if(numArrows > aliceArrows[n-1]) 
        {
            return dp[numArrows][n] = max(n-1 + helper(numArrows-aliceArrows[n-1]-1, aliceArrows, n-1),helper(numArrows, aliceArrows, n-1));
        } 
        else 
        {
            return dp[numArrows][n] = helper(numArrows, aliceArrows, n-1);
        }
    }
    
    vector<int> maximumBobPoints(int numArrows, vector<int>& aliceArrows) 
    {
        memset(dp, -1, sizeof dp);
        vector<int> ret(aliceArrows.size(), 0);
        helper(numArrows, aliceArrows, aliceArrows.size());
        for(int i = aliceArrows.size(); i > 0; i--) 
        {
            if(dp[numArrows][i] == dp[numArrows][i-1]) 
            {
                ret[i-1] = 0;
            } 
            else 
            {
                ret[i-1] = aliceArrows[i-1] + 1;
                numArrows -= (aliceArrows[i-1] + 1);
            }
        }
        ret[0] += numArrows;
        return ret;
    }
};
```
