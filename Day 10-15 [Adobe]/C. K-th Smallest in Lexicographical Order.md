# K-th Smallest in Lexicographical Order

Problem Link :- [Link](https://leetcode.com/problems/k-th-smallest-in-lexicographical-order/)

<h3>
Problem :- Given two integers n and k, return the kth lexicographically smallest integer in the range [1, n].
</h3>


**Solution :-**
```
class Solution {
public:
   int64_t count(int64_t n,int64_t j)
{
   
    if(j>n) return 0;
    
    if(j==n) return 1;
    
    int64_t mx_range=j,mn_range=j;
    int64_t ct=1;
    
    while(1)
    {
      mx_range=mx_range*10+9;
      mn_range=mn_range*10;
        
        if(mn_range >n) break;
       else if(mn_range<=n&&n<=mx_range)
        {
            ct += (n-mn_range+1);
           break;
        }
        else 
        {
            ct+=(mx_range-mn_range+1);
        }    
    }
    
    return ct;
}
    
    
   
int64_t findKthNumber(int64_t n, int64_t k,int64_t ct=0) 
{
    if(k>0)
   {
    for(int64_t i=(ct==0 ? 1 :0); i<=9; i++)
    {
        int64_t num =count(n,ct*10+i);
        
        if(num>=k) return findKthNumber (n,k-1,ct*10+i);
        k-=num;
        
    }
    }
    return ct;
}
};
```
