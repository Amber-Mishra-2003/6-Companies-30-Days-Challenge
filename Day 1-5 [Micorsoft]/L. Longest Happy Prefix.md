# Longest Happy Prefix

Problem Link :- [Link](https://leetcode.com/problems/longest-happy-prefix/description/)

<h3>
Problem :- A string is called a happy prefix if is a non-empty prefix which is also a suffix (excluding itself).
Given a string s, return the longest happy prefix of s. Return an empty string "" if no such prefix exists.  
</h3>



**Solution :-**

```
class Solution {
public:
    string longestPrefix(string str) {
        int l=str.length();
        int j=0;
        int i=1;
        vector<int>pre_arr(l,0);
        while(i<=l-1)
        {
            if(str[i]==str[j])
            {
                pre_arr[i]=j+1;
                j++;
                i++;
            }
            else{
                if(j==0)
                {
                    pre_arr[i]=0;
                    i++;
                }
                else if(j>0)
                {
                    j=pre_arr[j-1];
                }
            }
        }
        return str.substr(0,pre_arr[l-1]);
    }
};
```
