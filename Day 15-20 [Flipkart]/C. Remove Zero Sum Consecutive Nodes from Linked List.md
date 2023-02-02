# Remove Zero Sum Consecutive Nodes from Linked List

Problem Link :- [Link](https://leetcode.com/problems/remove-zero-sum-consecutive-nodes-from-linked-list/description/)

<h3>
Problem :- Given the head of a linked list, we repeatedly delete consecutive sequences of nodes that sum to 0 until there are no such sequences.

After doing so, return the head of the final linked list.  You may return any such answer.

(Note that in the examples below, all sequences are serializations of ListNode objects.)


</h3>


**Solution :-**
```
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode() : val(0), next(nullptr) {}
 *     ListNode(int x) : val(x), next(nullptr) {}
 *     ListNode(int x, ListNode *next) : val(x), next(next) {}
 * };
 */

class Solution {
public:
    ListNode* removeZeroSumSublists(ListNode* head) {
        unordered_map<int,ListNode*> m;
        ListNode* ptr=head;int prep=0;
        ListNode *dummy=new ListNode (0,head);
        m[0]=dummy;
        while(ptr!=NULL)
        {prep=prep+ptr->val;
            if(m.find(prep)!=m.end())
            { auto it=m[prep]->next;
             int SUM=prep;
             while(it!=ptr)
             {SUM+=it->val;
                 m.erase(SUM);
              it=it->next;
             }
                m[prep]->next=ptr->next;    
            }
            else
              m[prep]=ptr;
            ptr=ptr->next;   
        }
        return dummy->next;  
    }
};
```
