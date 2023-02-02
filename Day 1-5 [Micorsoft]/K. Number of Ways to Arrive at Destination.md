# Number of Ways to Arrive at Destination

Problem Link :- [Link](https://leetcode.com/problems/number-of-ways-to-arrive-at-destination/description/)

<h3>
Problem :- You are in a city that consists of n intersections numbered from 0 to n - 1 with bi-directional roads between some intersections. The inputs are generated such that you can reach any intersection from any other intersection and that there is at most one road between any two intersections.

  
  
You are given an integer n and a 2D integer array roads where roads[i] = [ui, vi, timei] means that there is a road between intersections ui and vi that takes timei minutes to travel. You want to know in how many ways you can travel from intersection 0 to intersection n - 1 in the shortest amount of time.

Return the number of ways you can arrive at your destination in the shortest amount of time. Since the answer may be large, return it modulo 109 + 7.
</h3> 




**Solution :-**

```
class Solution {
#define ll long long
public:
    int mod=1e9+7;
    int countPaths(int n, vector<vector<int>>& roads)
    {
        vector<pair<ll,ll>> adj[n];
    priority_queue<pair<ll,ll>,vector<pair<ll,ll>>,greater<pair<ll,ll>>> q;
        vector<ll> dis(n,LONG_MAX),ways(n,0);
         dis[0]=0;
        ways[0]=1;
      for(int i=0;i<roads.size();i++)
      { 
          adj[roads[i][0]].push_back({roads[i][1],roads[i][2]});
          adj[roads[i][1]].push_back({roads[i][0],roads[i][2]});
      }
        q.push({0,0}); 
        while(!q.empty()){
          ll prevtime=q.top().first;
          ll prevnode=q.top().second;
           q.pop();
          for(auto it:adj[prevnode]){
               ll newnode=it.first;
               ll newtime=it.second;
          if(dis[newnode]>prevtime+newtime)
              {
              dis[newnode]=prevtime+newtime;
              q.push({dis[newnode],newnode});
              ways[newnode]=ways[prevnode];
              }
        else if(dis[newnode]==prevtime+newtime){
          
           ways[newnode]=(ways[newnode]+ways[prevnode])%mod;
            }        
            }
            } 
      return ways[n-1];//ways to reach the last node
    }
};
```
