# Number of People Aware of a Secret

Problem Link :- [Link](https://leetcode.com/problems/number-of-people-aware-of-a-secret/)

<h3>
Problem :-On day 1, one person discovers a secret.

You are given an integer delay, which means that each person will share the secret with a new person every day, starting from delay days after discovering the secret. You are also given an integer forget, which means that each person will forget the secret forget days after discovering it. A person cannot share the secret on the same day they forgot it, or on any day afterwards.

Given an integer n, return the number of people who know the secret at the end of day n. Since the answer may be very large, return it modulo 109 + 7. 
</h3>


**Solution :-**
```
class Solution {
public:
    #define mod 1000000007
    int peopleAwareOfSecret(int n, int dl, int fg) {
        vector<int>dp(n+1,0);
        dp[0]=0;dp[1]=1;
        for(int i=1;i<=n;i++){
            for(int j=i+dl;j<=n && j<i+fg;j++){
                dp[j]=(dp[j]%mod+dp[i]%mod)%mod;
            }
            if(i+fg<=n)dp[i]=0;
        }
        int su=0;
        for(int i=0;i<=n;i++)su=(su%mod+dp[i]%mod)%mod;
        return su;
    }
    
};
```
