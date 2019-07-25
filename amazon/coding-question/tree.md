# Tree:

**103Binary Tree Zigzag Level Order Traversal**

在一个变量里面存level if level is even, reverse it use Collections.reverse\(list\);

```java
* Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    public List<List<Integer>> zigzagLevelOrder(TreeNode root) {
        List<List<Integer>> res = new ArrayList<>();
        if(root == null) return res;
        Queue<TreeNode> q = new LinkedList<>();
        q.add(root);
        int level = 0;
        while (!q.isEmpty()){
            level++;
           int size = q.size();
            List<Integer> list = new ArrayList<>();
           for (int i = 0; i < size; i++){
               TreeNode node = q.poll();
               list.add(node.val);
                if(node.left != null){
                    q.add(node.left);
                }
               if(node.right != null) q.add(node.right);
           }
            if(level % 2 == 0) Collections.reverse(list);
            res.add(list);
        }
        return res;
    }
}
// second methods
//use list.add(0, list); add to the index 0;
class Solution {
    public List<List<Integer>> zigzagLevelOrder(TreeNode root) {
        List<List<Integer>> res = new ArrayList<>();
        if(root == null) return res;
        Queue<TreeNode> q = new LinkedList<>();
        q.add(root);
        int level = 0;
        while (!q.isEmpty()){
            level++;
           int size = q.size();
            List<Integer> list = new ArrayList<>();
           for (int i = 0; i < size; i++){
               
               TreeNode node = q.poll();
               
              if( level % 2 == 0) list.add(0, node.val);
               else list.add(node.val);
                if(node.left != null){
                    q.add(node.left);
                }
               if(node.right != null) q.add(node.right);
           }
            
            res.add(list);
        }
        return res;
    }
}

```

**102Binary Tree Level Order Traversal**

使用queue 和 BFS 做 level, 一层一层的在queue里的

注意keep size of queue in top of while loop

```java

class Solution {
    public List<List<Integer>> levelOrder(TreeNode root) {
        List<List<Integer>> res = new ArrayList<>();
        if(root == null) return res;
        Queue<TreeNode> q = new LinkedList<>();
        q.add(root);
        while(!q.isEmpty()){
            int size = q.size();
             List<Integer> list = new ArrayList<>();
            for (int i = 0; i < size; i++){
               TreeNode node = q.poll();
                list.add(node.val);
                if(node.left != null) q.add(node.left);
                if(node.right != null) q.add(node.right);
            }
            res.add(list);
        }
        return res;
    }
}
```

111Minimum Depth of Binary Tree

```java
// recusive 
// Method: keep minDeep variable by layers
// time complex : O(n)
// space complex : O(n)
class Solution {
    public int minDepth(TreeNode root) {
         if(root == null) return 0;
         if(root.left == null && root.right == null) return 1;
          int left = minDepth(root.left);
          int right = minDepth(root.right);
           if(root.left == null) return right + 1;
            if(root.right == null) return left + 1;
           return Math.min(left, right) + 1;
    }
}
```

314Binary Tree Vertical Order Traversal

build up a queue to store the treeNode layer by layer 

build up a queue to store the index of treenode and index of root equals to 0, for the left, reduce one and for right side add one 

also keep min and max value use int 

last for loop to build result from min index to max index 

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
 // space o(n) time o(n)
class Solution {
    public List<List<Integer>> verticalOrder(TreeNode root) {
        List<List<Integer>> res = new ArrayList<>();
        if(root == null) return res;
        Queue<TreeNode> q = new LinkedList<>();
        Queue<Integer> index = new LinkedList<>();
        Map<Integer, ArrayList<Integer>> map = new HashMap<>();
        int max = 0;
        int min = 0;
        q.add(root);
        index.add(0);
        while(!q.isEmpty()){
            TreeNode node = q.poll();
            int cur = index.poll();
            map.putIfAbsent(cur, new ArrayList());
            map.get(cur).add(node.val);
            if(node.left != null){
                min = Math.min(min, cur - 1);
                q.add(node.left);
                index.add(cur - 1);
            }
            if(node.right != null){
                max = Math.max(max, cur + 1);
                q.add(node.right);
                index.add(cur + 1);
            }
        }
        for (int i = min; i <= max; i++){
            res.add(map.get(i));
        }
        return res;
    }
}
```

545Boundary of Binary Tree

get left boundary leaf boundary and right boundary and add to result

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    List<Integer> nodes =  new ArrayList<>(1000);
    public List<Integer> boundaryOfBinaryTree(TreeNode root) {
        if(root == null) return nodes;
        nodes.add(root.val);
        leftBoudary(root.left);
        leaves(root.left);
        leaves(root.right);
        rightBoudary(root.right);
        return nodes;
    }
    public void leftBoudary(TreeNode root){
        if(root == null || (root.left == null && root.right == null)) return;
        nodes.add(root.val);
        if(root.left == null) leftBoudary(root.right);
        else leftBoudary(root.left);
    }
    public void rightBoudary(TreeNode root){
        if(root == null || (root.left == null && root.right == null)) return;
        if(root.right == null) rightBoudary(root.left);
        else rightBoudary(root.right);
        nodes.add(root.val);
    }
    public void leaves(TreeNode root){
        if(root == null) return;
        if(root.left == null && root.right == null) {
            nodes.add(root.val);
            return;
        }
        leaves(root.left);
        leaves(root.right);
    }
}
```

```text

```

