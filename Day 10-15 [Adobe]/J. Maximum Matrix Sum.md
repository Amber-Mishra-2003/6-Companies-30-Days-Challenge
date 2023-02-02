# Maximum Matrix Sum

Problem Link :- [Link](https://leetcode.com/problems/maximum-matrix-sum/)

<h3>
Problem :- You are given an n x n integer matrix. You can do the following operation any number of times:

  * Choose any two adjacent elements of matrix and multiply each of them by -1.
  
Two elements are considered adjacent if and only if they share a border.

Your goal is to maximize the summation of the matrix's elements. Return the maximum sum of the matrix's elements using the operation mentioned above.
</h3>


**Solution :-**
```
class Solution {
public:
    long long maxMatrixSum(vector<vector<int>>& matrix) {
    int min_value=INT_MAX;
    int carry=0;
    long long int sum=0;
    
    for(int i=0;i<matrix.size();i++)
    {
        for(int j=0;j<matrix[0].size();j++)
        {
            if(abs(matrix[i][j])<min_value) 
               min_value=abs(matrix[i][j]);
            if(matrix[i][j]<0)
            {
                carry=1-carry;
            }
            sum=sum+abs(matrix[i][j]);
        }
    }
    if(carry==1)
    {
      sum-=(2*min_value);  
    }
      return sum;
}
};
```
