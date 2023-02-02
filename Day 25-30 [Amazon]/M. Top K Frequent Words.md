# Top K Frequent Words

Problem Link :- [Link](https://leetcode.com/problems/top-k-frequent-words/)

<h3>
Problem :- Given an array of strings words and an integer k, return the k most frequent strings.

Return the answer sorted by the frequency from highest to lowest. Sort the words with the same frequency by their lexicographical order.
</h3>


**Solution :-**
```
class Solution {
public:
    static bool comp(const pair<int, string>&p1, const pair<int, string>&p2) {
        if(p1.first < p2.first) return true;
        else if(p1.first == p2.first) return p1.second > p2.second;
        else return false;
    }
    
    vector<string> topKFrequent(vector<string>& words, int k) {
        unordered_map<string, int> mp;
        for(auto it : words) mp[it]++;
        
        std::priority_queue< pair<int, string>, std::vector<pair<int, string>>, std::function<bool(pair<int, string>, pair<int, string>)> > pq(comp);
        for(auto it : mp) pq.push({it.second, it.first});
        
        vector<string> ans;
        for(int i = 1; i <= k; i++)
            ans.push_back(pq.top().second), pq.pop();
        return ans;    
    }
};
```
