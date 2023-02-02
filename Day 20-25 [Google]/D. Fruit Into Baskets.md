# Fruit Into Baskets

Problem Link :- [Link](https://leetcode.com/problems/fruit-into-baskets/)

<h3>
Problem :- You are visiting a farm that has a single row of fruit trees arranged from left to right. The trees are represented by an integer array fruits where fruits[i] is the type of fruit the ith tree produces.

You want to collect as much fruit as possible. However, the owner has some strict rules that you must follow:

  * You only have two baskets, and each basket can only hold a single type of fruit. There is no limit on the amount of fruit each basket can hold.
  
  * Starting from any tree of your choice, you must pick exactly one fruit from every tree (including the start tree) while moving to the right. The picked fruits must fit in one of your baskets.
  
  * Once you reach a tree with fruit that cannot fit in your baskets, you must stop.
  
Given the integer array fruits, return the maximum number of fruits you can pick.
</h3>


**Solution :-**

```
class Solution {
public:
    int totalFruit(vector<int>& tree) {
        vector<int> count(tree.size(), 0);
        int first=0, second=0, ret=0;
        
        int distinctCount = 0;
        while (second < tree.size()) {
            count[tree[second]]++;
            if (count[tree[second]] == 1) {
                distinctCount++;
            }
    
            if (distinctCount > 2) {
                ret = max(ret, second-first);
                while (distinctCount > 2) {
                    count[tree[first]]--;
                    if (count[tree[first]] == 0) {
                        distinctCount--;
                    }
                    first++;
                }
            }
            second++;
        }
        
        return max(ret, second-first);
    }
};
```
