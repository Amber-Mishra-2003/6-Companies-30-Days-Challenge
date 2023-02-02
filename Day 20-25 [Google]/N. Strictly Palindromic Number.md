# Strictly Palindromic Number

Problem Link :- [Link](https://leetcode.com/problems/strictly-palindromic-number/)

<h3>
Problem :- An integer n is strictly palindromic if, for every base b between 2 and n - 2 (inclusive), the string representation of the integer n in base b is palindromic.

Given an integer n, return true if n is strictly palindromic and false otherwise.

A string is palindromic if it reads the same forward and backward.
</h3>


**Solution :-**
```
1. Brute Force Approach

class Solution {
public:
    bool isStrictlyPalindromic(int n) {
        for (int b = 2; b < n - 1; b++)
        {
            string s = "";
            int m = n;
            while (m)
            {
                s += (m % b + '0');
                m /= b;
            }
            if (!isPalind(s))
                return false;
        }
        return true;
    }
    
private: 
    bool isPalind(string& s)
    {
        int i = 0, j = s.length() - 1;
        while (i < j)
        {
            if (s[i] != s[j])
                return false;
            i++;
            j--;
        }
        return true;
    }
};



2. Direct Solution

class Solution {
public:
    bool isStrictlyPalindromic(int n) {
        return false;
    }
};
```
