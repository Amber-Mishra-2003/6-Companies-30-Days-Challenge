# Most Profitable Path in a Tree

Problem Link :- [Link](https://leetcode.com/problems/most-profitable-path-in-a-tree/)


<h3>

Problem :-There is an undirected tree with n nodes labeled from 0 to n - 1, rooted at node 0. You are given a 2D integer array edges of length n - 1 where edges[i] = [ai, bi] indicates that there is an edge between nodes ai and bi in the tree.

At every node i, there is a gate. You are also given an array of even integers amount, where amount[i] represents:

  * the price needed to open the gate at node i, if amount[i] is negative, or,
  * the cash reward obtained on opening the gate at node i, otherwise.
  
  
The game goes on as follows:

  * Initially, Alice is at node 0 and Bob is at node bob.
  * At every second, Alice and Bob each move to an adjacent node. Alice moves towards some leaf node, while Bob moves towards node 0.
  * For every node along their path, Alice and Bob either spend money to open the gate at that node, or accept the reward. Note that:
     * If the gate is already open, no price will be required, nor will there be any cash reward.
     * If Alice and Bob reach the node simultaneously, they share the price/reward for opening the gate there. In other words, if the price to open the gate is c, then both Alice and Bob pay c / 2 each. Similarly, if the reward at the gate is c, both of them receive c / 2 each.
  * If Alice reaches a leaf node, she stops moving. Similarly, if Bob reaches node 0, he stops moving. Note that these events are independent of each other.
  
Return the maximum net income Alice can have if she travels towards the optimal leaf node. 

 </h3> 
  


**Solution :-**

```
class Solution
{
public:
    int mostProfitablePath(vector<vector<int>> &edges, int bob, vector<int> &amount)
    {
        int n = edges.size() + 1;
        vector<int> adj[n];

        for (auto &x : edges)
        {
            adj[x[0]].push_back(x[1]);
            adj[x[1]].push_back(x[0]);
        }
        vector<int> p(n, -1); 
        vector<int> t(n);   
        vector<int> vis(n);   

        queue<int> bq;
        bq.push(bob);
        t[bob] = 0;
        vis[bob] = 1;

        while (!bq.empty())
        {
            int x = bq.front();
            bq.pop();
            for (int y : adj[x])
            {
                if (vis[y] == true)
                    continue;
                p[y] = x;
                vis[y] = 1;
                t[y] = t[x] + 1;
                bq.push(y);
            }
        }
        set<int> st; 
        int node = 0;
        while (node != -1)
        {
            st.insert(node);
            node = p[node];
        }
    
        for (int i = 0; i < n; i++)
            if (st.find(i) == st.end())
                t[i] = -1;

        vis.assign(n, 0);
        queue<pair<int, pair<int, int>>> q;
        int ans = INT_MIN;
        q.push({0, {0, 0}});

        while (!q.empty())
        {
            auto node = q.front();
            q.pop();
            int x = node.first;        
            int ct = node.second.first;   
            int val = node.second.second; 

            if (vis[x] == true)
                continue;
            vis[x] = true;

            if (t[x] == -1)            
                val += amount[x];
            else if (ct == t[x])        
                val += amount[x] / 2;
            else if (ct < t[x])       
                val += amount[x];

            if (adj[x].size() == 1 && x != 0) 
                ans = max(ans, val);

            for (int y : adj[x])
                q.push({y, {ct + 1, val}});
        }
        return ans;
    }
};
```
