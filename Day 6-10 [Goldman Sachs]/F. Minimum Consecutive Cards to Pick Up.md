# Minimum Consecutive Cards to Pick Up

Problem Link :- [Link](https://leetcode.com/problems/minimum-consecutive-cards-to-pick-up/)

<h3>
Problem :- You are given an integer array cards where cards[i] represents the value of the ith card. A pair of cards are matching if the cards have the same value.

Return the minimum number of consecutive cards you have to pick up to have a pair of matching cards among the picked cards. If it is impossible to have matching cards, return -1.
</h3>


**Solution :-**
```
class Solution {
public:
    int minimumCardPickup(vector<int>& cards) 
    {
        int s=INT_MAX;
        map<int,int> p;
        for(int i=0;i<cards.size();i++)
        {
            if(p.count(cards[i])>0)
            {
                s=min(s,i-p[cards[i]]+1);
                p[cards[i]]=i;
            }
           else
           p[cards[i]]=i;
        }
        if(s==INT_MAX)
        return -1;
        return s;
    }
};
```
