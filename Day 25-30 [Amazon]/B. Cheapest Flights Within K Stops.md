# Cheapest Flights Within K Stops

Problem Link :- [Link](https://leetcode.com/problems/cheapest-flights-within-k-stops/)

<h3>
Problem :-There are n cities connected by some number of flights. You are given an array flights where flights[i] = [fromi, toi, pricei] indicates that there is a flight from city fromi to city toi with cost pricei.

You are also given three integers src, dst, and k, return the cheapest price from src to dst with at most k stops. If there is no such route, return -1. 
</h3>


**Solution :-**
```
class Solution {
public:
 
    template<typename T_a3, typename T_vector>
    void bellman_ford(T_a3 &g, T_vector &dist, int src, int mx_edges) {
        dist[src] = 0;
        for (int i = 0; i <= mx_edges; i++) {
            T_vector ndist = dist;
            for (auto x : g) {
                auto [from, to, cost] = x;
                ndist[to] = min(ndist[to], dist[from] + cost);
            }
            dist = ndist;
        }
    }
    
    int findCheapestPrice(int n, vector<vector<int>>& flights, int src, int dst, int k) {
        vector<array<int, 3>> g;
        vector<int> cost(n, 1e9);
        for (auto f : flights) g.push_back({f[0], f[1], f[2]});
        bellman_ford(g, cost, src, k);
        return cost[dst] == 1e9 ? -1 : cost[dst];
    }
};
```
