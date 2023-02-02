# Non-negative Integers without Consecutive Ones

Problme Link :- [Link](https://leetcode.com/problems/non-negative-integers-without-consecutive-ones/)

<h3>
Problem :- Given a positive integer n, return the number of the integers in the range [0, n] whose binary representations do not contain consecutive ones.
</h3>


**Solution :-**
```
class Solution {
public:
    int findIntegers(int num) {
        if(num<=1)
            return (1<<num);
        int bits = log2(num);
        int dp[bits+1];
        memset(dp,0,sizeof(dp));
        dp[0]=1;
        dp[1]=2;
        for(int i=2;i<=bits;i++){
            dp[i]=dp[i-1]+dp[i-2];
        }
        
        int ans=0,prev=0;
        while(bits>=0){
            if(num & (1<<bits)){
                ans+=dp[bits];
                if(prev){
                    ans--;
                    break;
                }
                prev=1;
            }
            else{
                prev=0;
            }
            bits--;
        }
        return ans+1;
    }
};
```
