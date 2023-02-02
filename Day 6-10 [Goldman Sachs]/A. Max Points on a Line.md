# Max Points on a Line

Problem Link :- [Link](https://leetcode.com/problems/max-points-on-a-line/)

<h3>
Problem :- Given an array of points where points[i] = [xi, yi] represents a point on the X-Y plane, return the maximum number of points that lie on the same straight line.
</h3>


**Solution :-**

```
class Solution {
public:
    int maxPoints(vector<vector<int>>& points) 
    {
        int n = points.size();
        int ans = 0;
        double slope;
        for(int i=0; i<n-1; i++)
        {
            unordered_map<double, int> count;
            for(int j=i+1; j<n; j++)
            {
                if (points[j][0] == points[i][0])
                {
                    slope = DBL_MAX;
                }
                else
                {
                    slope = (double)(points[j][1] - points[i][1])/(points[j][0]-points[i][0]);
                }
                count[slope]++;
            }
            for(auto& [_, cnt]: count)
            {
                if (ans<cnt)
                {
                    ans = cnt;
                }
            }
            
        }
        return ans+1;
        
    }
};
```
