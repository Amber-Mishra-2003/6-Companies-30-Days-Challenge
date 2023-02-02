# Get Biggest Three Rhombus Sums in a Grid

Problem Link :- [Link](https://leetcode.com/problems/get-biggest-three-rhombus-sums-in-a-grid/)

<h3>
Problem :- You are given an m x n integer matrix grid.

A rhombus sum is the sum of the elements that form the border of a regular rhombus shape in grid. The rhombus must have the shape of a square rotated 45 degrees with each of the corners centered in a grid cell. Below is an image of four valid rhombus shapes with the corresponding colored cells that should be included in each rhombus sum:
  
  <img src="https://assets.leetcode.com/uploads/2021/04/23/pc73-q4-desc-2.png" width="300" height="300">
  
Note that the rhombus can have an area of 0, which is depicted by the purple rhombus in the bottom right corner.

Return the biggest three distinct rhombus sums in the grid in descending order. If there are less than three distinct values, return all of them.

</h3>


**Solution :-**
```
class Solution {
public:
	vector<int> getBiggestThree(vector<vector<int>>& grid) {
		priority_queue<int> pq;
		int m = grid.size(), n = grid[0].size();

		for(int i=0; i<m; i++){
			for(int j=0; j<n; j++){
				for(int k=0; i+k<m && i-k>=0 && j+2*k<n; k++){
					int si=i, sj=j, ti=i-k, tj=j+k, di=i+k, dj=j+k, ri=i, rj = j+2*k;
					int s1=0, s2=0, s3=0, s4=0;
					for(int l=0;l<k;l++){
						s1 += grid[si-l][sj+l];                        
						s2 += grid[ti+l][tj+l];
						s3 += grid[ri+l][rj-l];
						s4 += grid[di-l][dj-l];
					}
					int s = s1+s2+s3+s4;
					pq.push(max(s,grid[i][j]));
				}
			}
		}

		vector<int> ans;
		while(!pq.empty() && ans.size()<3){
			if(!ans.empty() && pq.top() == ans.back()){
				pq.pop();                
			} else {
				ans.push_back(pq.top());
				pq.pop();   
			}
		}
		return ans;
	}
};
```
