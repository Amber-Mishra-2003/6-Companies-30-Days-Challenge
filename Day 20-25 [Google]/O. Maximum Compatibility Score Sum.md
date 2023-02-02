# Maximum Compatibility Score Sum

Problem Link :- [Link](https://leetcode.com/problems/maximum-compatibility-score-sum/)

<h3>
Problem :- There is a survey that consists of n questions where each question's answer is either 0 (no) or 1 (yes).

The survey was given to m students numbered from 0 to m - 1 and m mentors numbered from 0 to m - 1. The answers of the students are represented by a 2D integer array students where students[i] is an integer array that contains the answers of the ith student (0-indexed). The answers of the mentors are represented by a 2D integer array mentors where mentors[j] is an integer array that contains the answers of the jth mentor (0-indexed).

Each student will be assigned to one mentor, and each mentor will have one student assigned to them. The compatibility score of a student-mentor pair is the number of answers that are the same for both the student and the mentor.

  * For example, if the student's answers were [1, 0, 1] and the mentor's answers were [0, 0, 1], then their compatibility score is 2 because only the second and the third answers are the same.
  
You are tasked with finding the optimal student-mentor pairings to maximize the sum of the compatibility scores.

Given students and mentors, return the maximum compatibility score sum that can be achieved.
</h3>


**Solution :-**
```
class Solution {
public:
    int max_compatibility = 0;
    int total_questions = 0;
    vector<bool> available_mentors;
    int maxCompatibilitySum(vector<vector<int>>& students, vector<vector<int>>& mentors) {
        available_mentors.resize(mentors.size(), false);
        total_questions = students[0].size();
        backtrack(students, mentors, 0, 0);
        return max_compatibility;
    }
    
    void backtrack(vector<vector<int>> &s, vector<vector<int>> &m, int s_index, int compatibility_score)
    {
        if(s_index == s.size())
            if(compatibility_score > max_compatibility)
                max_compatibility = compatibility_score;
        
        for(int i = 0; i < m.size(); i++)
        {
            if(available_mentors[i] == false)
            {
                available_mentors[i] = true;
                
                int score = 0;
                for(int q = 0; q < total_questions; q++)
                    score += (s[s_index][q] == m[i][q]);
                backtrack(s, m, s_index+1, compatibility_score + score);
                
                available_mentors[i] = false;
            }
        }
    }
};
```
