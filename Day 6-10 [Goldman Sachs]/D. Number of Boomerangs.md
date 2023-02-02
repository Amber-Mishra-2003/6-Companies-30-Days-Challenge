# Number of Boomerangs

Problem Link :- [Link](https://leetcode.com/problems/number-of-boomerangs/)

<h3>
Problem :-You are given n points in the plane that are all distinct, where points[i] = [xi, yi]. A boomerang is a tuple of points (i, j, k) such that the distance between i and j equals the distance between i and k (the order of the tuple matters).

Return the number of boomerangs. 
</h3>


**Solution :-**
```
class Solution {
public:
    int numberOfBoomerangs(vector<vector<int>>& points) {
        if (points.size() < 3) return 0;
        
        int count = 0;
        unordered_map<int,int> m;
        unordered_map<int,int>::iterator iter;
        for (int i = 0; i < points.size(); i++) 
        {
            m.clear();
            for (int j = 0; j < points.size(); j++)
                if (i != j)
                    m[getdistance(points[i],points[j])]++;
            
            for(iter = m.begin();iter != m.end(); iter++) 
            {
                if (iter->second > 1) 
                    count += iter->second * (iter->second-1); 
            }
        }
        
        return count;
    }
    
    inline int getdistance(vector<int>& x, vector<int>& y)
    {
        return (x[0]-y[0])*(x[0]-y[0])+(x[1]-y[1])*(x[1]-y[1]);
    }
};
```
