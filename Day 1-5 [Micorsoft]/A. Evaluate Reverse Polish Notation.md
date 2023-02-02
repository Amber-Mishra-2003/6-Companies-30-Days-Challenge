# Evaluate Reverse Polish Notation

Problem Link : - [Link](https://leetcode.com/problems/evaluate-reverse-polish-notation/)

<h3>
You are given an array of strings tokens that represents an arithmetic expression in a Reverse Polish Notation.Evaluate the expression. Return an integer that represents the value of the expression.
</h3>



**Solution:-**
```C++

class Solution
{
public:
    long long evalRPN(vector<string>& tokens) 
    {
        string s = tokens.back();
        tokens.pop_back();
        if(s != "+" && s != "-" && s != "*" && s != "/")return stoi(s);
        else 
            {
            long long a = evalRPN(tokens);
            long long b = evalRPN(tokens);
            if(s == "+") return a + b;
            else if (s == "-") return b - a;
            else if (s == "/") return b / a;
            else return a * b;
        }
    }
};

```
