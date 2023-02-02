# IPO

Problem Link :- [Link](https://leetcode.com/problems/ipo/)

<h3>
Problem :- Suppose LeetCode will start its IPO soon. In order to sell a good price of its shares to Venture Capital, LeetCode would like to work on some projects to increase its capital before the IPO. Since it has limited resources, it can only finish at most k distinct projects before the IPO. Help LeetCode design the best way to maximize its total capital after finishing at most k distinct projects.

You are given n projects where the ith project has a pure profit profits[i] and a minimum capital of capital[i] is needed to start it.

Initially, you have w capital. When you finish a project, you will obtain its pure profit and the profit will be added to your total capital.

Pick a list of at most k distinct projects from given projects to maximize your final capital, and return the final maximized capital.

The answer is guaranteed to fit in a 32-bit signed integer.
</h3>


**Solution :-**
```
class Solution {
public:
    int findMaximizedCapital(int k, int w, vector<int>& profits, vector<int>& capital) 
    {
        vector<pair<int,int>> v;
        for(int i=0;i<profits.size();++i)
        {
            v.push_back({capital[i],profits[i]});
        }
        sort(v.begin(),v.end());
        int i=0;
        priority_queue<int> q;
        while(k--)
        {
            while(i<v.size())
            {
                if(v[i].first<=w)
                {
                    q.push(v[i].second);
                    i++;
                }
                else
                {
                    break;
                }
            }
            if(!q.empty())
            {
                w+=q.top();
                q.pop();
            }
        }
        return w;
    }
};
```
