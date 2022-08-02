Approach 1 : Iteratively

Initially, we can keep two pointers - a) current : pointing to head and b) previous : pointing to null.
While current pointer is not null, assign a  current pointer's next to temp pointer.
Point current pointer's next to prev pointer.
Assign previous pointer to current and current to temp.
In the end, return previous which will be pointing to the head

``` java
//T : O(n)
//S : O(n)
class Solution {
    public ListNode reverseList(ListNode head) {
        ListNode curr = head;
        ListNode prev = null;
        while(curr != null)
        {
            ListNode temp = curr.next;
            curr.next = prev ;   
            prev = curr;
            curr = temp;
        }
        return prev;
    }
}

```
Time Complexity :  `O(n)`
Space Complexity :  `O(1)`

Approach 2 : Recursively

```cpp
class Solution {
public:
    ListNode* reverseList(ListNode* head) {
        return revLL(head, nullptr);
    }
    
    ListNode* revLL(ListNode* head, ListNode* prev) {
        if (head == nullptr)
            return prev;
        ListNode* next = head->next;
        head->next = prev;
        prev = head;
        return revLL(next, prev);
    }
};
```