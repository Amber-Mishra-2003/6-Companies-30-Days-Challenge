# Maximum Consecutive Floors Without Special Floors

Problem Link :- [Link](https://leetcode.com/problems/maximum-consecutive-floors-without-special-floors/)

<h3>
Problem :- Alice manages a company and has rented some floors of a building as office space. Alice has decided some of these floors should be special floors, used for relaxation only.

You are given two integers bottom and top, which denote that Alice has rented all the floors from bottom to top (inclusive). You are also given the integer array special, where special[i] denotes a special floor that Alice has designated for relaxation.

Return the maximum number of consecutive floors without a special floor.

 
</h3>


**Solution :-**
```
class Solution {
public:
    int maxConsecutive(int bottom, int top, vector<int>& special) 
    {
        int size = special.size();
        
        sort(special.begin(),special.end());
        
        int maxCount = 0;
       
        for(int i=0;i<size-1;i++)maxCount = max(maxCount,special[i+1]-special[i]-1);
       
        return max({maxCount,special[0]-bottom,top-special[size-1]});
    }
};
```
