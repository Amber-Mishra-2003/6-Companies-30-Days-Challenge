# Find the Winner of the Circular Game

Problem Link :- [Link](https://leetcode.com/problems/find-the-winner-of-the-circular-game/)

<h3>
Problem :- There are n friends that are playing a game. The friends are sitting in a circle and are numbered from 1 to n in clockwise order. More formally, moving clockwise from the ith friend brings you to the (i+1)th friend for 1 <= i < n, and moving clockwise from the nth friend brings you to the 1st friend.

The rules of the game are as follows:

Start at the 1st friend.
  
Count the next k friends in the clockwise direction including the friend you started at. The counting wraps around the circle and may count some friends more than once.
  
The last friend you counted leaves the circle and loses the game.
  
If there is still more than one friend in the circle, go back to step 2 starting from the friend immediately clockwise of the friend who just lost and repeat.
  
Else, the last friend in the circle wins the game.
  
Given the number of friends, n, and an integer k, return the winner of the game.
</h3>


**Solution :-**
```
class Solution {
public:
    int findTheWinner(int n, int k) {
        ListNode *prev = NULL;
        int x = 1;
        
        for(int i=n; i>=1; i--){
            ListNode *temp = new ListNode(i);
            temp->next = prev;
            prev = temp;
        }
        
        ListNode *head = prev, *curr = prev;
        while(head->next != NULL) 
            head = head->next;
        head->next = prev;
        
        if(k == 1)
            return n; 
        
        while(n != 1){
            if(x == k-1){
                curr->next = curr->next->next; 
                x = 1;
                n--;
            }else
                x++;
            curr = curr->next;
        }
        
        return curr->val;
    }
};
```
