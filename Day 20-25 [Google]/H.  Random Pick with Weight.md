# Random Pick with Weight

Problem Link :- [Link](https://leetcode.com/problems/random-pick-with-weight/)

<h3>
Problem :-ou are given a 0-indexed array of positive integers w where w[i] describes the weight of the ith index.

You need to implement the function pickIndex(), which randomly picks an index in the range [0, w.length - 1] (inclusive) and returns it. The probability of picking an index i is w[i] / sum(w).

For example, if w = [1, 3], the probability of picking index 0 is 1 / (1 + 3) = 0.25 (i.e., 25%), and the probability of picking index 1 is 3 / (1 + 3) = 0.75 (i.e., 75%).
  
</h3>


**Solution :-**
```
class Solution {
public:
    Solution(vector<int>& w) {
       int s=0; 
       for(auto e:w) sum.push_back(s+=e); 
    }
    
    int pickIndex() {
        int x = rand() % sum.back();
        return upper_bound(sum.begin(), sum.end(), x) - sum.begin();
    }
    
private:
     vector<int> sum;
};
```
