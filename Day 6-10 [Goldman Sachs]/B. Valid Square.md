# Valid Square

Problem Link :- [Link](https://leetcode.com/problems/valid-square/description/)

<h3>
Problem :- Given the coordinates of four points in 2D space p1, p2, p3 and p4, return true if the four points construct a square.
  
The coordinate of a point pi is represented as [xi, yi]. The input is not given in any order.

A valid square has four equal sides with positive length and four equal angles (90-degree angles).
  
</h3>


**Solution :-**
```
class Solution {
public:
    int distance(vector<int> a1, vector<int> a2)
    {
        int distance= (a2[0]-a1[0])*(a2[0]-a1[0])+(a2[1]-a1[1])*(a2[1]-a1[1]);
        return distance;
    }
    
    
    bool validSquare(vector<int>& p1, vector<int>& p2, vector<int>& p3, vector<int>& p4) {
        
        int d1=distance(p1,p2);
        int d2=distance(p2,p3);
        int d3=distance(p3,p4);
        int d4=distance(p4,p1);
        int d5=distance(p1,p3);
        int d6=distance(p2,p4);
        
        vector<int> ans;
         ans.push_back(d1);
         ans.push_back(d2);
         ans.push_back(d3);
         ans.push_back(d4);
         ans.push_back(d5);
         ans.push_back(d6);
        
        sort(ans.begin(),ans.end());
        int i=0;
        int j=4;
            int flag=0;
        
        for(int i=0;i<6;i++){
            cout<<ans[i];
        }
        
        
        while(i<3){
            if(ans[i]==ans[i+1])
                flag=1;
            else if(ans[i]!=ans[i+1]){
                flag=0;
                break;
            }
            i++;
        }
        
       if(ans[4]==ans[5] && flag==1 && ans[0]!=ans[4])
           return true;
        
        else return false;
    }
};

```
