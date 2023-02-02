# Number of Closed Islands

Problem Link :- [Link](https://leetcode.com/problems/number-of-closed-islands/description/)

<h3>
Problem :- Given a 2D grid consists of 0s (land) and 1s (water).  An island is a maximal 4-directionally connected group of 0s and a closed island is an island totally (all left, top, right, bottom) surrounded by 1s.

Return the number of closed islands.
</h3>


**Solution :-**
```
class Solution {
public:
    int closedIsland(vector<vector<int>>& grid) {
        int res = 0;
        vector<vector<int>> visited(grid.size(),vector<int>(grid[0].size(),0));
        for(int i = 0 ; i < grid.size() ; i++){
            for(int j = 0 ; j < grid[0].size() ; j++){
                if(grid[i][j] == 0 && visited[i][j] == 0){
                    visited[i][j] = 1;
                    res += bfs(grid,visited,i,j);
                }
            }
        }
        return res;
    }
    int bfs(vector<vector<int>>& grid, vector<vector<int>>& visited,int x, int y){
        queue<pair<int,int>> myq;
        myq.push(make_pair(x,y));
        int dir[4][2] = {{1,0},{-1,0},{0,1},{0,-1}};
        int res = true;
        while(myq.size()){
            int size = myq.size();
            for(int i = 0 ; i < size ; i++,myq.pop()){
                auto it = myq.front();
                if(it.first == 0 || it.first == grid.size()-1 || it.second == 0 || it.second == grid[0].size()-1)
                    res = false;
                for(int j = 0 ; j < 4 ; j++){
                    int x_ = it.first + dir[j][0];
                    int y_ = it.second + dir[j][1];
                    if((x_ >= 0 && x_ < grid.size() && y_ >= 0 && y_ < grid[0].size()) && grid[x_][y_] == 0 && visited[x_][y_] == 0){
                        visited[x_][y_] = 1;
                        myq.push(make_pair(x_,y_));
                    }
                }
            }
        }
        return res;
    }
};
```
