# Pattern 07: Tree Breadth First Search
### Binary Tree Level Order Traversal (easy)
https://leetcode.com/problems/binary-tree-level-order-traversal/
```java
public List<List<Integer>> levelOrder(TreeNode root) {
        Queue<TreeNode> queue = new LinkedList<>();
        List<List<Integer>> ans = new LinkedList<>();
        if(root==null){
            return ans;
        }
        queue.offer(root);
        while(!queue.isEmpty()){
            int level = queue.size();
            List<Integer> sublist = new LinkedList<>();
            for(int i=0;i<level;i++){
                TreeNode node = queue.peek();
                if(node.left!=null){
                    queue.offer(node.left);
                }
                if(node.right!=null){
                    queue.offer(node.right);
                }
                sublist.add(queue.poll().val);
            }
            ans.add(sublist);
        }
        return ans;
    }
```
Each node is visited exactly once, so the time complexity is (O(n)), where (n) is the number of nodes in the tree.
Space Complexity:
The queue stores at most one level of the tree at any time. In the worst case (a balanced tree), this is (O(w)), where (w) is the maximum width of the tree.
### Reverse Level Order Traversal (easy)
https://leetcode.com/problems/binary-tree-level-order-traversal-ii/
```java
public void traversal(TreeNode root, List<List<Integer>> list, int level){
        if(root==null){
            return;
        }
        if(level>=list.size()){
            list.add(0,new ArrayList());
        }
        traversal(root.left,list,level+1);
        traversal(root.right,list,level+1);
        list.get(list.size()-1-level).add(root.val);
    }
    public List<List<Integer>> levelOrderBottom(TreeNode root) {
        List<List<Integer>> ans = new LinkedList<>();
        if(root==null){
            return ans;
        }
        traversal(root,ans,0);
        return ans;
    }
```
```java
public List<List<Integer>> levelOrderBottom(TreeNode root) {
        Queue<TreeNode> queue = new LinkedList<>();
        List<List<Integer>> ans = new LinkedList<>();
        if(root==null){
            return ans;
        }
        queue.offer(root);
        while(!queue.isEmpty()){
            int level = queue.size();
            List<Integer> sublist = new LinkedList<>(); 
            for(int i=0;i<level;i++){
                TreeNode node = queue.peek();
                if(node.left!=null){
                    queue.offer(node.left);
                }
                if(node.right!=null){
                    queue.offer(node.right);
                }
                sublist.add(queue.poll().val);
            }
            ans.addFirst(sublist);
        }
        return ans;
    }
```
### Zigzag Traversal (medium)
https://leetcode.com/problems/binary-tree-zigzag-level-order-traversal/
```java
public List<List<Integer>> zigzagLevelOrder(TreeNode root) {
        Queue<TreeNode> queue = new LinkedList<>();
        List<List<Integer>> ans = new LinkedList<>();
        int r=0;
        if(root==null){
            return ans;
        }
        queue.offer(root);
        while(!queue.isEmpty()){
            int level = queue.size();
            List<Integer> sublist = new LinkedList<>(); 
            for(int i=0;i<level;i++){
                TreeNode node = queue.peek();
                if(node.left!=null){
                    queue.offer(node.left);
                }
                if(node.right!=null){
                    queue.offer(node.right);
                }
                if(r==0){
                sublist.addLast(queue.poll().val);
                }else{
                sublist.addFirst(queue.poll().val);
                }
            }
            ans.add(sublist);
            r=r==0?1:0;
        }
        return ans;
    }
````
### Level Averages in a Binary Tree (easy)
https://leetcode.com/problems/average-of-levels-in-binary-tree/
```java
public List<Double> averageOfLevels(TreeNode root) {
        Queue<TreeNode> queue = new LinkedList<>();
        List<Double> ans = new LinkedList<>();
        if(root==null){
            return ans;
        }
        queue.offer(root);
        while(!queue.isEmpty()){
            int level = queue.size();
            double value =0;
            for(int i=0;i<level;i++){
                if(queue.peek().left!=null){
                queue.offer(queue.peek().left);
                }
                if(queue.peek().right!=null){
                    queue.offer(queue.peek().right);
                }
                value +=queue.poll().val;
            }
            ans.add(value/level);
        }
        return ans; 
    }
```
### Level Maximum in a Binary Tree
https://leetcode.com/problems/maximum-level-sum-of-a-binary-tree/
```java
public int maxLevelSum(TreeNode root) {
        Queue<TreeNode> queue = new LinkedList<>();
        if(root==null){
            return 1;
        }
        queue.offer(root);
        int l=0;
        int mlevel=Integer.MIN_VALUE, msum=Integer.MIN_VALUE;
        while(!queue.isEmpty()){
            int level=queue.size();
            l++;
            int sum=0;
            for(int i=0;i<level;i++){
                TreeNode node = queue.peek();
                if(node.left!=null){
                    queue.offer(node.left);
                }
                if(node.right!=null){
                    queue.offer(node.right);
                }
                sum+=queue.poll().val;
            }
            if(sum>msum){
                    msum=sum;
                    mlevel=l;
                }
        }
        return mlevel==Integer.MIN_VALUE?1:mlevel;
    }
```
### Minimum Depth of a Binary Tree (easy)
https://leetcode.com/problems/minimum-depth-of-binary-tree/
```java
public int minDepth(TreeNode root) {
        Queue<TreeNode> queue = new LinkedList<>();
        if(root==null){
            return 0;
        }
        queue.offer(root);
        int l=0;
        int mlevel=1;
        while(!queue.isEmpty()){
            int level=queue.size();
            l++;
            for(int i=0;i<level;i++){
                TreeNode node = queue.poll();
                if (node.left == null && node.right == null) return l;
                if(node.left!=null){
                    queue.offer(node.left);
                }
                if(node.right!=null){
                    queue.offer(node.right);
                }
            }
        }
        return -1;
    }
```

### Maximum Depth of a Binary Tree
https://leetcode.com/problems/maximum-depth-of-binary-tree/
```java
public int maxDepth(TreeNode root) {
        Queue<TreeNode> queue = new LinkedList<>();
        if(root==null){
            return 0;
        }
        queue.offer(root);
        int l=0;
        while(!queue.isEmpty()){
            int level=queue.size();
            l++;
            for(int i=0;i<level;i++){
                TreeNode node = queue.poll();
                if(node.left!=null){
                    queue.offer(node.left);
                }
                if(node.right!=null){
                    queue.offer(node.right);
                }
            }
        }
        return l;
    }
```
### Connect Level Order Siblings (medium)
https://leetcode.com/problems/populating-next-right-pointers-in-each-node/
```java
public Node connect(Node root) {
        if (root == null)
            return null;
        Node temp=root;
        while(temp.left!=null){
            Node curr=temp;
            while(curr!=null){
                curr.left.next=curr.right;
                if(curr.next!=null){
                    curr.right.next=curr.next.left;
                }
                curr=curr.next;
                
            }
            temp=temp.left;
        }
        return root;
    }
```
