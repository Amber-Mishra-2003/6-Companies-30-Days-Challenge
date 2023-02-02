# Matrix Block Sum

Problem Link :- [Link](https://leetcode.com/problems/matrix-block-sum/)

<h3>
Problem :- Given a m x n matrix mat and an integer k, return a matrix answer where each answer[i][j] is the sum of all elements mat[r][c] for:

  * i - k <= r <= i + k,
  
  * j - k <= c <= j + k, and
  
  * (r, c) is a valid position in the matrix.
</h3>
  

**Solution :-**
```
class Solution {
public:
  vector<vector<int>> matrixBlockSum(vector<vector<int>> &mat, int K) {
  int n = mat.size();
  if (n == 0)
    return {{}};
  int m = mat[0].size();

  vector<vector<int>> prefix(mat), answer(mat);

 
  for (auto i = 1; i < n; i++)
    prefix[i][0] = prefix[i][0] + prefix[i - 1][0];
  for (auto j = 1; j < m; j++)
    prefix[0][j] = prefix[0][j] + prefix[0][j - 1];
  for (auto i = 1; i < n; i++)
    for (auto j = 1; j < m; j++)
      prefix[i][j] = prefix[i][j] + prefix[i - 1][j] + prefix[i][j - 1] -prefix[i - 1][j - 1];

  
  for (auto i = 0; i < n; i++) {
    for (auto j = 0; j < m; j++) {
      auto range_end_i = min(i + K, n - 1);
      auto range_end_j = min(j + K, m - 1);
      answer[i][j] = prefix[range_end_i][range_end_j];

      if (i - K - 1 >= 0 && j - K - 1 >= 0)
        answer[i][j] += prefix[i - K - 1][j - K - 1] -prefix[range_end_i][j - K - 1] -prefix[i - K - 1][range_end_j];
      else if (i - K - 1 >= 0)
        answer[i][j] -= prefix[i - K - 1][range_end_j];
      else if (j - K - 1 >= 0)
        answer[i][j] -= prefix[range_end_i][j - K - 1];
    }
  }

  return answer;
}
};
```
