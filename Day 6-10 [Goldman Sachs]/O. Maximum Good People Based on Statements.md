# Maximum Good People Based on Statements

Problem Link :- [Link](https://leetcode.com/problems/maximum-good-people-based-on-statements/)

<h3>
Problem :- There are two types of persons:

  * The good person: The person who always tells the truth.
  * The bad person: The person who might tell the truth and might lie.
  
  
You are given a 0-indexed 2D integer array statements of size n x n that represents the statements made by n people about each other. More specifically, statements[i][j] could be one of the following:

  * 0 which represents a statement made by person i that person j is a bad person.
  * 1 which represents a statement made by person i that person j is a good person.
  * 2 represents that no statement is made by person i about person j.
  
  
Additionally, no person ever makes a statement about themselves. Formally, we have that statements[i][i] = 2 for all 0 <= i < n.
</h3>


**Solution :-**
```
class Solution {
public:
    int helper(int mask,vector<int> &roles)
    {
        int count=0;
        int n=roles.size();
        for(int i=0;i<n;i++)
        {
            if(mask&1)
            {
                roles[i]=1;
                count++;
            }
            else
            roles[i]=0;
            mask>>=1;
        }
        return count;
    }
    bool valid(vector<int> &roles,vector<vector<int> > &statements)
    {
        int n=roles.size();
        for(int i=0;i<n;i++)
        {
            if(roles[i]==0)
            continue;
            for(int j=0;j<n;j++)
            {
                if(statements[i][j]==2)
                continue;
                if(statements[i][j]!=roles[j])
                return false;
            }
        }
        return true;
    }
    int maximumGood(vector<vector<int>>& statements) {
        int n=statements[0].size();
        int combinations=1<<n;
        vector<int> roles(n);
        int ans=0;
        for(int i=1;i<=combinations;i++)
        {
            int currentGood=helper(i,roles);
            if(valid(roles,statements))
            {
                ans=max(ans,currentGood);
            }
        }
        return ans;
    }
};
```
