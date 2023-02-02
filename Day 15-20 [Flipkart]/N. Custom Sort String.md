# Custom Sort String

Problem Link :- [Link](https://leetcode.com/problems/custom-sort-string/)

<h3>
Problem :- You are given two strings order and s. All the characters of order are unique and were sorted in some custom order previously.

Permute the characters of s so that they match the order that order was sorted. More specifically, if a character x occurs before a character y in order, then x should occur before y in the permuted string.

Return any permutation of s that satisfies this property.
</h3>


**Solution :-**
```
class Solution {
public:
    string customSortString(string S, string T) {
        vector<int> weight(26, 0);
        int cur_weight(25);
        for (char c : S) {
            weight[c - 'a'] = cur_weight--;
        }
        
        vector<string> char_buckets(26, "");
        
        for (char c : T) {
            char_buckets[weight[c - 'a']].push_back(c);
        }
        
        ostringstream oss;
        for (int weight = 25; weight >= 0; --weight) {
            oss << char_buckets[weight];
        }
        
        return oss.str();
    }
};
```
