# Swim in Rising Water

Problem Link :- [Link](https://leetcode.com/problems/swim-in-rising-water/)

<h3>
Problem :- You are given an n x n integer matrix grid where each value grid[i][j] represents the elevation at that point (i, j).

The rain starts to fall. At time t, the depth of the water everywhere is t. You can swim from a square to another 4-directionally adjacent square if and only if the elevation of both squares individually are at most t. You can swim infinite distances in zero time. Of course, you must stay within the boundaries of the grid during your swim.

Return the least time until you can reach the bottom right square (n - 1, n - 1) if you start at the top left square (0, 0).
</h3>


**Solution :-**
```
class Solution {
public:
    int n;
    int swimInWater(vector<vector<int>>& grid) {
        n = grid.size();
        int mx = 0;
        if( n == 0) return 0;
        for(auto &vec : grid) {
            for(auto num : vec)
                mx = max(mx, num);
        }
        int l = 0, r = mx;
        while(l < r) {
            int mid = (l+r) / 2;
            set<pair<int, int> > m;
            if(dfs(grid, 0, 0, mid, m))
                r = mid;
            else
                l = mid + 1;
        }
        return r;
    }
    
    bool dfs(vector<vector<int>>& grid, int x, int y, int h, set<pair<int, int> > &m) {
        if(x < 0 || y < 0 || x >= n || y >= n || m.count({x, y}) || grid[x][y] > h) return false;
        if( x == n - 1 && y == n - 1) return true;
        m.insert({x, y});
        return dfs(grid, x + 1, y, h, m) ||
            dfs(grid, x, y + 1, h, m) ||
            dfs(grid, x - 1, y, h, m) ||
            dfs(grid, x, y - 1, h, m);
    }
};
```
