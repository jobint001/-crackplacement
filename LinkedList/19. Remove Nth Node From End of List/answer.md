Given the head of a linked list, remove the nth node from the end of the list and return its head.

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
    ListNode* removeNthFromEnd(ListNode* head, int n) {

        stack<ListNode*> st;
        ListNode*  temp=head;

        while(temp!=nullptr){
            st.push(temp);
            temp=temp->next;
        }
        ListNode* item;
      while(n>1){
        item=st.top();
        st.pop();
        
        n--;
      }
      st.pop();
      if(!st.empty()){
        cout<<st.top()->val;
        st.top()->next=item;
      } else{
       ListNode* t= new ListNode(0);
       head=item;
      }
      
       return head;
    }
};
```
