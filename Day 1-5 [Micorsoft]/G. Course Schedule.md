# Course Schedule

Problem Link :- [Link](https://leetcode.com/problems/course-schedule/)

<h3>
Problem : - There are a total of numCourses courses you have to take, labeled from 0 to numCourses - 1. You are given an array prerequisites where prerequisites[i] = [ai, bi] indicates that you must take course bi first if you want to take course ai.

* For example, the pair [0, 1], indicates that to take course 0 you have to first take course 1.
  
Return true if you can finish all courses. Otherwise, return false.
</h3> 




**Solution : -**

```
class Solution
{
public:

    bool dfs(vector<bool> &vis, vector<bool> &recst, vector<vector<int>> &pre, int i)
    {
        vis[i] = true;
        recst[i] = true;
        for (auto &j : pre[i])
        {
            bool temp = false;
            if (recst[j])
            {
                return true;
            }
            else if (!vis[j])
            {
                temp = dfs(vis, recst, pre, j);
                if (temp)
                {
                    return true;
                }
            }
        }
        recst[i] = false;
        return false;
    }
bool canFinish(int num, vector<vector<int>> &prereq)
{
    
    vector<vector<int>> pre(num);
    for (auto &i : prereq)
    {
        int x = i[0], y = i[1];
        pre[y].push_back(x);
    }
    vector<bool> vis(num + 1, false);
    vector<bool> recst(num + 1, false);
    bool temp = false;
    for (int i = 0; i < num; i++)
    {
        if (!vis[i])
        {
            temp = dfs(vis, recst, pre, i); 
            if (temp)
            {
                return false;
            }
        }
    }
    return true;
}
};

```
