# Generate Random Point in a Circle

Problem Link :- [Link](https://leetcode.com/problems/generate-random-point-in-a-circle/)

<h3>
Problem :- Given the radius and the position of the center of a circle, implement the function randPoint which generates a uniform random point inside the circle.

Implement the Solution class:

  * Solution(double radius, double x_center, double y_center) initializes the object with the radius of the circle radius and the position of the center (x_center, y_center).
  
  * randPoint() returns a random point inside the circle. A point on the circumference of the circle is considered to be in the circle. The answer is returned as an array [x, y].
</h3>


**Solution :-**
```
class Solution {
public:
    double r,x,y;
    Solution(double radius, double x_center, double y_center) {
        r = radius;
        x = x_center;
        y = y_center;
    }
    
    vector<double> randPoint() {
        double x_r = ((double)rand()/RAND_MAX * (2*r)) + (x-r);
        double y_r = ((double)rand()/RAND_MAX * (2*r)) + (y-r);
        
        while(solve(x_r,y_r,x,y)>=r*r)
        {
            x_r = ((double)rand()/RAND_MAX * (2*r)) + (x-r);
            y_r = ((double)rand()/RAND_MAX * (2*r)) + (y-r);
        }
        
        return {x_r,y_r};
    }
    
    double solve(double x_r,double y_r,double x,double y)
    {
        return (x-x_r)*(x-x_r) + (y-y_r)*(y-y_r);
    }
};
```
