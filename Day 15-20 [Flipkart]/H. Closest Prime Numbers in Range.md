# Closest Prime Numbers in Range

Problem Link :- [Link](https://leetcode.com/problems/closest-prime-numbers-in-range/)

<h3>
Problem :- Given two positive integers left and right, find the two integers num1 and num2 such that:

  * left <= nums1 < nums2 <= right .
                                 
  * nums1 and nums2 are both prime numbers.
                                 
  * nums2 - nums1 is the minimum amongst all other pairs satisfying the above conditions.
                                 
Return the positive integer array ans = [nums1, nums2]. If there are multiple pairs satisfying these conditions, return the one with the minimum nums1 value or [-1, -1] if such numbers do not exist.

A number greater than 1 is called prime if it is only divisible by 1 and itself.
</h3>


**Solution :-**
```
class Solution {
public:
bool isPrime(int n){
    if(n == 0 ||n == 1 ){
        return false;
    }
    for(int i = 2;  i*i <= n ; i++ ){
        if(n%i == 0)return false;

    }
    return true;
}
    vector<int> closestPrimes(int left, int right) {
        int prev = 0;
        vector<int> ans ;
        for(int i = left ; i<= right ; i++){
            if(isPrime(i)){
                if(ans.size() < 2){
                    ans.push_back(i);
                }else{
                    if(ans[1] - ans[0] > i - prev){
                        ans[0] = prev;
                        ans[1] = i;
                    }
                    else if(ans[1] - ans[0] > i - ans[1]){
                        ans[0] = ans[1];
                        ans[1] = i;
                    }else{
                        prev = i;
                    }
                    
                }
            }
        }
        if(ans.size()==2){
            return ans;
        }
        return {-1 , -1};
    }
};
```
