# Shopping Offers

Problem Link :- [Link](https://leetcode.com/problems/shopping-offers/)

<h3>
Problem :- In LeetCode Store, there are n items to sell. Each item has a price. However, there are some special offers, and a special offer consists of one or more different kinds of items with a sale price.

You are given an integer array price where price[i] is the price of the ith item, and an integer array needs where needs[i] is the number of pieces of the ith item you want to buy.

You are also given an array special where special[i] is of size n + 1 where special[i][j] is the number of pieces of the jth item in the ith offer and special[i][n] (i.e., the last integer in the array) is the price of the ith offer.

Return the lowest price you have to pay for exactly certain items as given, where you could make optimal use of the special offers. You are not allowed to buy more items than you want, even if that would lower the overall price. You could use any of the special offers as many times as you want.
</h3>


**Solution :-**
```
class Solution {
public:
    int ans=INT_MAX;
    void dfs(vector<int>& price, vector<vector<int>>& special, vector<int>& needs,vector<int>& curr,int cost){
        for(int i=0;i<curr.size();i++){
            if(curr[i]<0) return;
        }
        if(needs==curr){
            if(cost<ans){
                ans=cost;
                return;
            }
        }
        if(cost>=ans) return;
        for(int i=0;i<special.size();i++){
            bool possible = true;
            for(int j=0;j<special[i].size()-1;j++){
                if(special[i][j]+curr[j]>needs[j]){
                    possible =false;
                    break;
                }
            }
            if(possible){
                vector<int> temp=curr;
                for(int j=0;j<special[i].size()-1;j++){
                    curr[j]+=special[i][j];
                }
                int x=special[i].size();
                dfs(price,special,needs,curr,cost+special[i][x-1]);
                curr=temp;
            }
        }
        vector<int> temp=curr;
        int t=0;
        for(int i=0;i<curr.size();i++){
            t+=(needs[i]-curr[i])*price[i];
        }
        dfs(price,special,needs,needs,cost+t);
        curr=temp;
    }
    
    int shoppingOffers(vector<int>& price, vector<vector<int>>& special, vector<int>& needs) {
        int n=price.size();
        if(n==0) return 0;
        vector<int> curr(n,0);
        dfs(price,special,needs,curr,0);
        return ans;
    }
};
```
