Approach :

Add the right side node in the queue before adding the left side nodes. This way whenever we are iterating over the queue, the value at index 0 will be the value of the right side node, thereby following the FIFO principle. If the right side node is not present, the view from right side will show the left element
```java
class Solution {
    public List<Integer> rightSideView(TreeNode root) {
        List<Integer> result = new ArrayList<>();
        if(root == null)
            return result;
        
        Queue<TreeNode> queue = new LinkedList<>();
        queue.offer(root);
        
        while(!queue.isEmpty()) {
            int level = queue.size();
            for(int i = 0; i< level; i++){
                TreeNode curr = queue.poll();
                
                if(i == 0)
                    result.add(curr.val);
                
                if(curr.right != null)
                    queue.offer(curr.right);
                if(curr.left != null)
                    queue.offer(curr.left);
                
            }
        }
        return result;
    }
}
```
Time : O(N)
Space : O(N)