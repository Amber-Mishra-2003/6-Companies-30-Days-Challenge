# Perfect Rectangle

Problem Link :- [Link](https://leetcode.com/problems/perfect-rectangle/)

<h3>
Problem : - Given an array rectangles where rectangles[i] = [xi, yi, ai, bi] represents an axis-aligned rectangle. The bottom-left point of the rectangle is (xi, yi) and the top-right point of it is (ai, bi).
Return true if all the rectangles together form an exact cover of a rectangular region.
</h3>



**Solution :-**

```
class Solution {
public:
    bool isRectangleCover(vector<vector<int>>& rectangles) 
    {
       long long  area=0;
       long long int xmin=INT_MAX;
       long long int xmax=INT_MIN;
       long long int ymin=INT_MAX;
       long long int ymax=INT_MIN;
        multiset<pair<int,int>>st;
        for(auto u:rectangles)
        {
            xmin=min(xmin,u[0]*1ll);
            
            ymin=min(ymin,u[1]*1ll);
            
            xmax=max(xmax,u[2]*1ll);
            
            ymax=max(ymax,u[3]*1ll);
            
            area+=((u[2]-u[0])*1ll*(u[3]-u[1]))*1ll;
            
            if(st.find({u[0],u[1]})!=st.end())
                st.erase({u[0],u[1]});  
                
            else st.insert({u[0],u[1]});  
        
            if(st.find({u[0],u[3]})!=st.end())
                st.erase({u[0],u[3]});  
                
            else st.insert({u[0],u[3]});
            
            if(st.find({u[2],u[1]})!=st.end())
                st.erase({u[2],u[1]});
                
            else st.insert({u[2],u[1]});
            
            if(st.find({u[2],u[3]})!=st.end())
                st.erase({u[2],u[3]});
                
            else st.insert({u[2],u[3]});
        }
       
        if(st.find({xmin,ymin})==st.end()||st.find({xmin,ymax})==st.end()||st.find({xmax,ymin})==st.end()||st.find({xmax,ymax})==st.end()|| st.size()!=4)
                  return false;  
                  
        return area==(xmax-xmin)*(ymax-ymin); 
    }
};


```
