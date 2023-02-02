# Max Area of Island

Problem Link :- [Link](https://leetcode.com/problems/max-area-of-island/)

<h3>
Problem :- You are given an m x n binary matrix grid. An island is a group of 1's (representing land) connected 4-directionally (horizontal or vertical.) You may assume all four edges of the grid are surrounded by water.

The area of an island is the number of cells with a value 1 in the island.

Return the maximum area of an island in grid. If there is no island, return 0.
</h3>


**Solution :-**
```
class Solution {
public:
    int dfs(int x,int y,int n,int m,vector<vector<int>> &grid, vector<vector<int>> &dp){
    
	
    if(dp[x][y] != -1)  return dp[x][y];
    grid[x][y] = -1;
    int px[4] = {-1,0,0,1};
    int py[4] = {0,-1,1,0};
    int s = 0;
    for(int i=0; i<4; i++){
        int p = x + px[i];
        int q = y + py[i];
        if(p>=0 && p<n && q>=0 && q<m && grid[p][q] == 1)   
				  s += 1 + dfs(p,q,n,m,grid,dp);
    }
    dp[x][y] = s; 
    return s;
}

int maxAreaOfIsland(vector<vector<int>>& grid) {
    
    if(grid.empty())    return 0;
    int n = grid.size();
    int m = grid[0].size();
    vector <vector<int>> dp(n,vector<int>(m,-1)); 
    int l = -1;
    for(int i=0; i<n; i++){
        for(int j=0; j<m; j++){
            if(grid[i][j] == 1){
                int c = dfs(i,j,n,m,grid,dp);
                l = max(l,c);
            }
        }
    }
    return (l+1);
    
}
};
```
