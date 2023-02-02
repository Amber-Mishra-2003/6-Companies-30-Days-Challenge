# Query Kth Smallest Trimmed Number

Problem Link :- [Link](https://leetcode.com/problems/query-kth-smallest-trimmed-number/)

<h3>
Problem :- You are given a 0-indexed array of strings nums, where each string is of equal length and consists of only digits.

You are also given a 0-indexed 2D integer array queries where queries[i] = [ki, trimi]. For each queries[i], you need to:

  * Trim each number in nums to its rightmost trimi digits.
  
  * Determine the index of the kith smallest trimmed number in nums. If two trimmed numbers are equal, the number with the lower index is considered to be smaller.
  
  * Reset each number in nums to its original length.
  
  * Return an array answer of the same length as queries, where answer[i] is the answer to the ith query.

Note:

  * To trim to the rightmost x digits means to keep removing the leftmost digit, until only x digits remain.
  
  * Strings in nums may contain leading zeros.
</h3>


**Solution :-**
```
class Solution {
public:
    vector<int> smallestTrimmedNumbers(vector<string>& nums, vector<vector<int>>& queries) {
        
        vector<int> vc;
        for(int i=0;i<queries.size();++i)
        {
            int x=queries[i][0];
            int y=queries[i][1];
            priority_queue<pair<string,int>, vector <pair<string, int>>, greater<pair<string, int>>> pq;
            int j=0;
            for(auto s:nums)
            {
               pq.push({s.substr(s.length()-y,s.length()),j});
               j++;
            }
            int k=1;
            while(k<x)
            {
                pq.pop();
                k++;
            }
            vc.push_back(pq.top().second);
        }
        return vc;
    }
};
```
