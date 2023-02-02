# Number of Substrings Containing All Three Characters

Problem Link :- [Link](https://leetcode.com/problems/number-of-substrings-containing-all-three-characters/)

<h3>
Problem :- Given a string s consisting only of characters a, b and c.
Return the number of substrings containing at least one occurrence of all these characters a, b and c.
  
</h3>


**Solution :-**
```
class Solution {
public:
    int numberOfSubstrings(string s) {
        int n = s.size();
        int l = 0,r = 0,last = n-1;
        int cnt = 0;
        vector<int> vt(3,0);
        while(r<n)
        {
            vt[s[r]-'a']++;
            while(vt[0] && vt[1] && vt[2])
            {
                cnt += (1 + (last - r));
                vt[s[l]-'a']--;
                l++;
            }
            r++;
        }
        return cnt;
    }
};

```
