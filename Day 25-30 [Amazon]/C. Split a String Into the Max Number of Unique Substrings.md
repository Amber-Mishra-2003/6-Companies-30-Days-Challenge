# Split a String Into the Max Number of Unique Substrings

Problem Link :- [Link](https://leetcode.com/problems/split-a-string-into-the-max-number-of-unique-substrings/)

<h3>
Problem :- Given a string s, return the maximum number of unique substrings that the given string can be split into.

You can split string s into any list of non-empty substrings, where the concatenation of the substrings forms the original string. However, you must split the substrings such that all of them are unique.

A substring is a contiguous sequence of characters within a string.
</h3>


**Solution :-**
```
class Solution {
public:
    int max_unique_substrings(string s,unordered_set<string>&seen)
    {
        int maximum = 0;
        for(int i = 1;i<s.length() + 1;i++)
        {
            string candidate = s.substr(0,i);
            if(seen.count(candidate) == 0)
            {
                seen.insert(candidate);
                maximum = max(maximum, 1 + max_unique_substrings(s.substr(i),seen));
                seen.erase(candidate);
            }
        }
        return maximum;
    }
    int maxUniqueSplit(string s) {
        unordered_set<string> seen;
        return max_unique_substrings(s,seen);
    }
};
```
