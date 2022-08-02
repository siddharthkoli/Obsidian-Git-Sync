Approach:

1. Assign the given node value to next node value
2. Assign node's next to the node's next's next value
For eg. 4, 5, 1, 9 ---> 4, 1, 1, 9 ----> 4, 1, 
```java
public void deleteNode(ListNode node) {
        if(node != null && node.next != null)
        {
            node.val = node.next.val;
            node.next = node.next.next;
        }
    }
```
Time:
Space: