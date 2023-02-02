# Maximum Length of Repeated Subarray

Problem Link :- [Link](https://leetcode.com/problems/maximum-length-of-repeated-subarray/description/)

<h3>
Problem :- Given two integer arrays nums1 and nums2, return the maximum length of a subarray that appears in both arrays.
</h3>


**Solution :-**
```
class Solution {
public:
     int findLength(vector<int>& A, vector<int>& B) {
        int m=A.size();
        int n=B.size();
        int dp[m+1][n+1];
        for(int i=0;i<m;i++)
            dp[i][0]=0;
        for(int i=0;i<n;i++)
            dp[0][i]=0;
        int maxi=INT_MIN;
        for(int i=1;i<m+1;i++)
        {
            for(int j=1;j<n+1;j++)
            {
                if(A[i-1]==B[j-1])
                    dp[i][j]=dp[i-1][j-1]+1;
                else
                    dp[i][j]=0;
                maxi=max(maxi,dp[i][j]);
            }
        }
        return maxi;
    }
};
```
