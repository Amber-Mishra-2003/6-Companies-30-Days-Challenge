# Check If a String Contains All Binary Codes of Size K

Problem Link :- [Link](https://leetcode.com/problems/check-if-a-string-contains-all-binary-codes-of-size-k/description/)

<h3>
Problem :- Given a binary string s and an integer k, return true if every binary code of length k is a substring of s. Otherwise, return false.
</h3>


**Solution :-**
```
class Solution {
public:
    bool hasAllCodes(string s, int k) {
         unordered_map<string,int> mp; 
    
    if(s.size() < k)
        return false;
    
    string temp="";
    
    for(int i=0;i<k;i++)
    {
        temp+=s[i];
    }
    mp[temp]++;
    for(int i=k;i<s.size();i++)
    {
        temp+=s[i];    
        temp.erase(temp.begin()+0); 
        mp[temp]++;   
    }
    long long a=pow(2,k);
    if(mp.size()!=a)
        return false;
    return true;
    }
};
```
