# Network Delay Time

Problem Link :- [Link](https://leetcode.com/problems/network-delay-time/)

<h3>
Problem :- You are given a network of n nodes, labeled from 1 to n. You are also given times, a list of travel times as directed edges times[i] = (ui, vi, wi), where ui is the source node, vi is the target node, and wi is the time it takes for a signal to travel from source to target.

We will send a signal from a given node k. Return the minimum time it takes for all the n nodes to receive the signal. If it is impossible for all the n nodes to receive the signal, return -1.
</h3>


**Solution:-**
```
class Solution {
public:
    int networkDelayTime(vector<vector<int>>& times, int N, int K) {
        unordered_map<int, unordered_map<int, int>> graph;
        for (auto& time : times)
            graph[time[0]][time[1]] = time[2];
        
        vector<int> cost(N, INT_MAX);
        cost[K-1] = 0;
        
        set<pair<int, int>> s;
        s.insert({0, K});
        
        while (!s.empty()) {
            int u = s.begin()->second; 
            s.erase(s.begin());
            
            for (auto& entry : graph[u]) {
                int v = entry.first;
                int weight = entry.second;
            
                if (cost[u-1]+weight < cost[v-1]) {
                   
                    if (cost[v-1] != INT_MAX) 
                        s.erase(s.find({cost[v-1], v}));
                    cost[v-1] = cost[u-1]+weight;
                    s.insert({cost[v-1], v});
                }
            }
        }
        
        int ret = 0;
        for (int c : cost)
            ret = max(ret, c);

        return ret == INT_MAX ? -1 : ret;
    }
};
```
