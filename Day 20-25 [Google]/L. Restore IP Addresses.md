# Restore IP Addresses

Problem Link :- [Link](https://leetcode.com/problems/restore-ip-addresses/)

<h3>
Problem :-A valid IP address consists of exactly four integers separated by single dots. Each integer is between 0 and 255 (inclusive) and cannot have leading zeros.

  * For example, "0.1.2.201" and "192.168.1.1" are valid IP addresses, but "0.011.255.245", "192.168.1.312" and "192.168@1.1" are invalid IP addresses.
  
Given a string s containing only digits, return all possible valid IP addresses that can be formed by inserting dots into s. You are not allowed to reorder or remove any digits in s. You may return the valid IP addresses in any order.

  
</h3>


**Solution :-**
```
class Solution {
    vector<string> ans;
public:
    void restoreDFS(string s, string temp, int dot, int index) {
        if (index == s.size() and dot == 4) {
            temp.pop_back();
            ans.push_back(move(temp));
            return;
        }
        if (index >= s.size() or dot >= 4) {
            return;
        }
		
        
        restoreDFS(s, temp + s[index] + '.', dot + 1, index + 1);
		
		
        if (s[index] != '0') {
            restoreDFS(s, temp + s.substr(index, 2) + '.', dot + 1, index + 2);
        }
		
		
        if (s[index] != '0' and (stoi(s.substr(index, 3)) < 256)) {
            restoreDFS(s, temp + s.substr(index, 3) + '.', dot + 1, index + 3);
        }
    }
    
    vector<string> restoreIpAddresses(string s) {
        if (s.size() > 12 or s.size() < 4) return ans;
        restoreDFS(s, "", 0, 0);
        return ans;
    }
};
```
