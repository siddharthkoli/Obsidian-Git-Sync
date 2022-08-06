Approach 1: Brute Force
1. Calculate the total number of nodes in a linked list
2. Calculate the mid of the linked list 
3. Traverse through the list until you do not reach the mid
4. In case, count is 0, return null. If count is 1, return head.

``` java
public ListNode middleNode(ListNode head) {
        ListNode curr = head;
        int count = 0;
        
        while(curr != null)
        {
            count++;
            curr = curr.next;
        }
        
        if(count == 0)
            return null;
        if(count == 1)
            return head;
        
        curr = head;
        int mid = count/2;
        for(int i = 0; i<mid; i++)
        {
            curr = curr.next;
        }
        return curr;
    }

```
Time:
Space:
<hr/>
Approach 2: Fast and Slow Pointers

If we move slow pointer by 1 step each, and fast pointer by 2 steps, when fast pointer reaches at the end, slow pointer will 
