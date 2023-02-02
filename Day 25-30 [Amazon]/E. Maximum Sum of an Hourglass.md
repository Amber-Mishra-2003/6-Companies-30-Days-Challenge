# Maximum Sum of an Hourglass

Problem Link :- [Link](https://leetcode.com/problems/maximum-sum-of-an-hourglass/)

<h3>
Problem :- You are given an m x n integer matrix grid.

We define an hourglass as a part of the matrix with the following form:
  
<img src="https://assets.leetcode.com/uploads/2022/08/21/img.jpg" alt="Girl in a jacket" width="300" height="300">
  
Return the maximum sum of the elements of an hourglass.

Note that an hourglass cannot be rotated and must be entirely contained within the matrix.
</h3>


**Solution :-**
```
class Solution {
public:
    int maxSum(vector<vector<int>>& grid) {
        int max_sum = 0;
        for(int i = 0;i<grid.size()-2;i++)
        {
            for(int j = 0;j<grid[0].size()-2;j++)
            {
                int sum = grid[i][j]+grid[i][j+1]+grid[i][j+2]+grid[i+1][j+1]+grid[i+2][j]+grid[i+2][j+1]+grid[i+2][j+2];
                if(sum>max_sum)
                    max_sum = sum;
            }
        }
        return max_sum;
    }
};
```
