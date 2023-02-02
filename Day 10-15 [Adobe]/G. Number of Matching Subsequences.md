# Number of Matching Subsequences

Problem Link :- [Link](https://leetcode.com/problems/number-of-matching-subsequences/)

<h3>
Problem :- Given a string s and an array of strings words, return the number of words[i] that is a subsequence of s.

A subsequence of a string is a new string generated from the original string with some characters (can be none) deleted without changing the relative order of the remaining characters.

* For example, "ace" is a subsequence of "abcde".
</h3>


**Solution :-**
```
class Solution {
public:
    
    bool check(string s,string t){
        int count=0;
        int j=0;
        for(int i=0;i<t.size();i++)
        {
            if(t[i]==s[j])
            {
                j++;
                count++;
            }
            if(count==s.size())
        {
            return true;
                break;
        }
        }
        
        return false;
    }
    
    int numMatchingSubseq(string s, vector<string>& words) {
        int ans=0;
        unordered_map<string,int> m;
        for(int i=0;i<words.size();i++)
        {
            m[words[i]]++;
        }
        for(auto x:m)
        {
            if(check(x.first,s))
                ans+=x.second;
        }
        return ans;
    }
};

    
```
