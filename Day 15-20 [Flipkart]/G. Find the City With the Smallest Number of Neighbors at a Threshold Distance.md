# Find the City With the Smallest Number of Neighbors at a Threshold Distance

Problem Link :- [Link](https://leetcode.com/problems/find-the-city-with-the-smallest-number-of-neighbors-at-a-threshold-distance/)

<h3>
Problem :-There are n cities numbered from 0 to n-1. Given the array edges where edges[i] = [fromi, toi, weighti] represents a bidirectional and weighted edge between cities fromi and toi, and given the integer distanceThreshold.

Return the city with the smallest number of cities that are reachable through some path and whose distance is at most distanceThreshold, If there are multiple such cities, return the city with the greatest number.

Notice that the distance of a path connecting cities i and j is equal to the sum of the edges' weights along that path.

  
</h3>


**Solution :-**
```
class Solution {
public:
    int findTheCity(int n, vector<vector<int>>& edges, int distanceThreshold) {

      int k=distanceThreshold;
      vector<pair<int,int>> adj[n];
      for(auto it:edges){
           adj[it[0]].push_back({it[1],it[2]});
           adj[it[1]].push_back({it[0],it[2]});
       }

       int max=-1,ans;

      for(int i=0;i<n;i++)
      {
        priority_queue<pair<int,int>,vector<pair<int,int>>,greater<pair<int,int>>>pq;
        vector<int>dist(n,1e9);

        pq.push({0,i});
        dist[i]=0;

        while(!pq.empty())
        {
          int node=pq.top().second;
          int dis=pq.top().first;
          pq.pop();

          for(auto it:adj[node])
          {
            int adjnode=it.first;
            int edw=it.second;
            if(dist[adjnode]>dis+edw && dis+edw<=k)
            {
              dist[adjnode]=dis+edw;
              pq.push({dis+edw,adjnode});
            }
          }
        }

        int c=0;

        for(int j=0;j<n;j++)
        {
          if(dist[j]==1e9)
          {
            c++;
          }
        }
        

        if(max<=c){
        max=c;
        ans=i;
        }

      }

      return ans;
        
    }
};
```
