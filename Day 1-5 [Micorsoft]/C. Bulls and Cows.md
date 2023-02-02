# Bulls and Cows

Problem Link : - [Link](https://leetcode.com/problems/bulls-and-cows/)

<h3>
Problem : - You are playing the Bulls and Cows game with your friend.You write down a secret number and ask your friend to guess what the number is. When your friend makes a guess, you provide a hint with the following info:

    * The number of "bulls", which are digits in the guess that are in the correct position.
    * The number of "cows", which are digits in the guess that are in your secret number but are located in the wrong position. Specifically, the non-bull digits in the guess that could be rearranged such that they become bulls.
  
Given the secret number secret and your friend's guess guess, return the hint for your friend's guess.

The hint should be formatted as "xAyB", where x is the number of bulls and y is the number of cows. Note that both secret and guess may contain duplicate digits.
</h3>



**Solution : -**
```
class Solution 
{
public:
    string getHint(string secret, string guess) 
    {
        int as =0;
        int bs =0;
        std::map<char , int> hashmap{};
        for(char a: secret)
        {
            hashmap[a]++;
        }
        
        for(int i=0; i < guess.size() ; i++)
        {
            if(guess[i] == secret[i])
            {
                if(hashmap[guess[i]] > 0)
                {
                    as++;
                    hashmap[guess[i]]--;
                }
                else
                {
                    bs--;
                    as++;
                }
            }
            else if(hashmap.count(guess[i]) > 0 && hashmap[guess[i]] > 0)
            {
                bs++;
                hashmap[guess[i]]--;
            }
        }
        
        string ans = to_string(as) + 'A' + to_string(bs) + 'B';
        
        return ans;
        
    }
};

```
