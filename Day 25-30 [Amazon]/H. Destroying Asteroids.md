# Destroying Asteroids

Problem Link :- [Link](https://leetcode.com/problems/destroying-asteroids/)

<h3>
Problem :- You are given an integer mass, which represents the original mass of a planet. You are further given an integer array asteroids, where asteroids[i] is the mass of the ith asteroid.

You can arrange for the planet to collide with the asteroids in any arbitrary order. If the mass of the planet is greater than or equal to the mass of the asteroid, the asteroid is destroyed and the planet gains the mass of the asteroid. Otherwise, the planet is destroyed.

Return true if all asteroids can be destroyed. Otherwise, return false.
</h3>


**Solution :-**
```
class Solution {
public:
    bool asteroidsDestroyed(int mass, vector<int>& asteroids) {
        
        sort(begin(asteroids), end(asteroids));
        
        long long sum = mass;
        
        for(int i: asteroids){
            
            long long num = i;
            
            if(num > sum)
                return false;
            
            sum += num;
        }
        
        return true;
    }
};
```
