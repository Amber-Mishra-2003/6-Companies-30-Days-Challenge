# Maximum Number of Coins You Can Get

Problem Link :- [Link](https://leetcode.com/problems/maximum-number-of-coins-you-can-get/description/)

<h3>
Problem :- There are 3n piles of coins of varying size, you and your friends will take piles of coins as follows:

  * In each step, you will choose any 3 piles of coins (not necessarily consecutive).
  
  * Of your choice, Alice will pick the pile with the maximum number of coins.
  
  * You will pick the next pile with the maximum number of coins.
  
  * Your friend Bob will pick the last pile.
  
  * Repeat until there are no more piles of coins.
  
Given an array of integers piles where piles[i] is the number of coins in the ith pile.

Return the maximum number of coins that you can have.
</h3>


**Solution :-**
```
class Solution {
public:
    int maxCoins(vector<int>& piles) {
        sort(piles.begin(),piles.end());
        int n=piles.size();
        int i=0,j=n-1,k=n-2;
        int ans=0;
        while(i<k){
            ans+=piles[k];
            i++;
            k-=2;
            j-=2;
        }
        return ans;
    }

};
```
