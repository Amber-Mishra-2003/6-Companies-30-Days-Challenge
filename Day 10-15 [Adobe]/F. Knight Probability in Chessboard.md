# Knight Probability in Chessboard

Problem Link :- [Link](https://leetcode.com/problems/knight-probability-in-chessboard/)

<h3>
Problem :- On an n x n chessboard, a knight starts at the cell (row, column) and attempts to make exactly k moves. The rows and columns are 0-indexed, so the top-left cell is (0, 0), and the bottom-right cell is (n - 1, n - 1).

A chess knight has eight possible moves it can make, as illustrated below. Each move is two cells in a cardinal direction, then one cell in an orthogonal direction.
</h3>

<img src="https://assets.leetcode.com/uploads/2018/10/12/knight.png">


**Solution :-**
```
class Solution {
private:
    double dp[25][25][101] = {0};
public:
    double knightProbability(int n, int k, int row, int column) {
        int x, y;
        double ans = 0;
        int dirx[] = {-2, -1, 1, 2, 2, 1, -1, -2};
        int diry[] = {1, 2, 2, 1, -1, -2, -2, -1};
        dp[row][column][0] = 1;
        for (int a = 0; a < k; ++a)
            for (int i = 0; i < n; ++i)
                for (int j = 0; j < n; ++j)
                    if (dp[i][j][a] > 0) {
                        for (int b = 0; b < 8; ++b) {
                            x = i + dirx[b];
                            y = j + diry[b];
                            if (x >= 0 && x < n && y >= 0 && y < n)
                                dp[x][y][a+1] += dp[i][j][a]/8;
                        }
                    }
        for (int i = 0; i < n; ++i)
            for (int j = 0; j < n; ++j)
                ans += dp[i][j][k];
        return ans;
    }
};
```
