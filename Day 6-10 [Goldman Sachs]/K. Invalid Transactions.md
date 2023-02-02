# Invalid Transactions

Problem Link :- [Link](https://leetcode.com/problems/invalid-transactions/)

<h3>
Problem :- A transaction is possibly invalid if:

  * the amount exceeds $1000, or;
  * if it occurs within (and including) 60 minutes of another transaction with the same name in a different city.
You are given an array of strings transaction where transactions[i] consists of comma-separated values representing the name, time (in minutes), amount, and city of the transaction.

Return a list of transactions that are possibly invalid. You may return the answer in any order.
</h3>


**Solution :-**
```
class Solution {
public:
    vector<string> delim(string a){
        vector<string> cur;
        string str = "";
        for (auto& c : a){
            if (c == ','){
                cur.push_back(str);
                str = "";
            }
            else str += c;
        }
        cur.push_back(str);
        return cur;
    }
    vector<string> invalidTransactions(vector<string>& t) {
        vector<string> ans;
        vector<bool> v(t.size());
        unordered_map<string, vector<vector<string>>> m;
        for (int i = 0; i < t.size(); ++i){
            vector<string> ts = delim(t[i]);
            for (auto& vc : m[ts[0]]){
                if (vc[3] != ts[3] && abs(stoi(vc[1]) - stoi(ts[1])) <= 60){
                    if(!v[stoi(vc[4])]) {
                        ans.push_back(vc[5]);
                        v[stoi(vc[4])] = true;
                    }
                    if(!v[i]){
                        ans.push_back(t[i]);
                        v[i] = true;
                    }
                }
            }
            ts.push_back(to_string(i));
            ts.push_back(t[i]);
            m[ts[0]].push_back(ts);
            if (!v[i] && stoi(ts[2]) > 1000) {
                v[i] = true;
                ans.push_back(t[i]);
            }
        }
        return ans;
    }
};
```
