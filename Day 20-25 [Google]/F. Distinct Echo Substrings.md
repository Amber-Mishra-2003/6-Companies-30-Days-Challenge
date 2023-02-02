# Distinct Echo Substrings

Problem Link :- [Link](https://leetcode.com/problems/distinct-echo-substrings/)

<h3>
Problem :- Return the number of distinct non-empty substrings of text that can be written as the concatenation of some string with itself (i.e. it can be written as a + a where a is some string).
</h3>


**Solution :-**
```
class Solution {
public:
    int distinctEchoSubstrings(string text) {
        vector<int> alp(26,-1);
        vector<int> hmap(text.size(), -1);
        for(int i=0; i<text.size(); i++){
            hmap[i] = alp[text[i]-'a'];   
            alp[text[i]-'a'] = i;
        }
        unordered_set<string> hset;
        vector<int> consec(26,0);
        
        int res = 0;
        for(int i=0; i<text.size(); i++){
            if(hmap[i]==-1) continue;
            int cur = i;
            while(cur>=0 && text.at(cur)==text.at(i))
                cur--;     
            consec[text.at(i)-'a'] = max(consec[text.at(i)-'a'], i-cur);
            cur++;
            int ind = hmap[cur];
            while(ind!=-1){
                if(ind+1< i-ind)    break;
                int dis = i - ind;
                string s1 = text.substr(ind-(dis-1), dis);
                string s2 = text.substr(ind+1, dis);
                if(s1==s2 && !hset.count(s1)){
                    hset.insert(s1);
                    res++;
                }
                ind = hmap[ind];
            }
        }
        
        for(int ele:consec) 
            res += ele/2;
        return res;
    }
};
```
