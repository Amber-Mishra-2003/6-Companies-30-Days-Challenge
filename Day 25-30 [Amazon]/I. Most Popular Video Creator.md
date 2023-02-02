# Most Popular Video Creator

Problem Link :- [Link](https://leetcode.com/problems/most-popular-video-creator/)

<h3>
Problem :- You are given two string arrays creators and ids, and an integer array views, all of length n. The ith video on a platform was created by creator[i], has an id of ids[i], and has views[i] views.

The popularity of a creator is the sum of the number of views on all of the creator's videos. Find the creator with the highest popularity and the id of their most viewed video.

  * If multiple creators have the highest popularity, find all of them.
  
  * If multiple videos have the highest view count for a creator, find the lexicographically smallest id.
  
Return a 2D array of strings answer where answer[i] = [creatori, idi] means that creatori has the highest popularity and idi is the id of their most popular video. The answer can be returned in any order.
</h3>


**Solution :-**
```
class Solution {
public:
    vector<vector<string>> mostPopularCreator(vector<string>& creators, vector<string>& ids, vector<int>& views) {
        vector<vector<string>> ans;
        map<string,long long> mapViews,orginalViews;
        map<string,string> mapids;
        long long popular=0;
        int len = creators.size();
        for(int i=0;i<len;i++){
            mapViews[creators[i]]+=views[i];
            popular = max(popular,mapViews[creators[i]]);
            if(views[i]>orginalViews[creators[i]] || orginalViews[creators[i]]==0)          {
                orginalViews[creators[i]] = views[i];
                mapids[creators[i]] = ids[i];   
            } else if(views[i]==orginalViews[creators[i]]){
                mapids[creators[i]] = min(mapids[creators[i]] ,ids[i]);   
            }
        }
        
        for(auto & mv:mapViews){
            if(mv.second==popular){
                ans.push_back({mv.first,mapids[mv.first]});
            }
        }   
        return ans;
    }
};
```
