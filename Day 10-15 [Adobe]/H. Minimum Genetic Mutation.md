# Minimum Genetic Mutation

Problem Link :- [Link](https://leetcode.com/problems/minimum-genetic-mutation/)

<h3>
Problem :- A gene string can be represented by an 8-character long string, with choices from 'A', 'C', 'G', and 'T'.

Suppose we need to investigate a mutation from a gene string startGene to a gene string endGene where one mutation is defined as one single character changed in the gene string.

  * For example, "AACCGGTT" --> "AACCGGTA" is one mutation.
  
There is also a gene bank bank that records all the valid gene mutations. A gene must be in bank to make it a valid gene string.

Given the two gene strings startGene and endGene and the gene bank bank, return the minimum number of mutations needed to mutate from startGene to endGene. If there is no such a mutation, return -1.

Note that the starting point is assumed to be valid, so it might not be included in the bank.
</h3>


**Solution :-**
```
class Solution {
public:
    int minMutation(string start, string end, vector<string>& bank) {
        unordered_map<char,int> mp;
        mp['A'] = 1;
        mp['C'] = 1;
        mp['G'] = 1;
        mp['T'] = 1;
        
        int res=0;
        queue<string> q;
        unordered_set<string> st(bank.begin(),bank.end()); 
        
        q.push(start);
        
        while(!q.empty()){
            int size = q.size();
            for(int i=0;i<size;i++){
                string word = q.front();
                q.pop();
                st.erase(word);
                
                if(word == end) return res;
                
                for(int j=0;j<word.length();j++){
                    char ch = word[j];
                    for(auto it:mp){
                        word[j] = it.first;
                        
                        if(st.count(word)>0){
                            q.push(word);
                            st.erase(word);
                        }
                    }
                    word[j] = ch;
                }
            }
            res++;
        }
        
        return -1;
    }
};
```
