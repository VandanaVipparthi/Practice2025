# Pattern 08:Tree Depth First Search
### Binary Tree Path Sum (easy)
https://leetcode.com/problems/path-sum/
```java
public boolean dfs(TreeNode root, int targetSum,int sum){
        if(root==null){
            return false;
        }
        sum+=root.val;
        if(root.left==null && root.right==null){
            return sum==targetSum;
        }
        return dfs(root.left,targetSum,sum) || dfs(root.right,targetSum,sum);
    }
    public boolean hasPathSum(TreeNode root, int targetSum) {
        return dfs(root,targetSum,0);
    }
```
### All Paths for a Sum (medium)
https://leetcode.com/problems/path-sum-ii/
```java
class Solution {
    public void dfs(TreeNode root, int targetSum, int csum, List<Integer> path, List<List<Integer>> output){
        if(root==null){
            return ;
        }
        csum+=root.val;
        path.add(root.val);
        if(root.left==null && root.right==null && csum==targetSum){
            output.add(new ArrayList<>(path));
        }
        dfs(root.left,targetSum,csum,path,output);
        dfs(root.right,targetSum,csum,path,output);
        path.remove(path.size()-1);
    }
    public List<List<Integer>> pathSum(TreeNode root, int targetSum) {
        List<List<Integer>> ans = new ArrayList<>(); 
        dfs(root,targetSum,0,new ArrayList<>(),ans);
        return ans;
    }
}
```
### Given a binary tree, return all root-to-leaf paths.
https://leetcode.com/problems/binary-tree-paths/
```java
public void dfs(TreeNode root, List<String> ans, String path){
        if(root==null){
            return;
        }
        if(path!=""){
            path+="->";
        }
        path+=String.valueOf(root.val);
        if(root.right==null && root.left==null){
            ans.add(path);
        }
        dfs(root.left,ans,path);
        dfs(root.right,ans,path);

    }
    public List<String> binaryTreePaths(TreeNode root) {
        List<String> ans = new ArrayList<>();
        dfs(root,ans,"");
        return ans;
    }
```
### Sum of Path Numbers (medium)
https://leetcode.com/problems/sum-root-to-leaf-numbers/
```java
public int dfs(TreeNode root, int ans,String path){
        if(root==null){
            return 0;
        }
        path+=String.valueOf(root.val);
        if(root.left==null && root.right==null){
            ans+=Integer.valueOf(path);
            return ans;
        }
        return dfs(root.left,ans,path)+dfs(root.right,ans,path);
        
    }
    public int sumNumbers(TreeNode root) {
        return dfs(root,0,"");
         
    }
```
### Count Paths for a Sum (medium)
https://leetcode.com/problems/path-sum-iii/
```java
public int func(TreeNode root, int ts, long csum, HashMap<Long,Integer> map){
        if(root==null){
            return 0;
        }
        csum+=root.val;
        int count=map.getOrDefault(csum-ts,0);
        map.put(csum,map.getOrDefault(csum,0)+1);
        count+=func(root.left,ts,csum,map);
        count+=func(root.right,ts,csum,map);
        //backtracking
        map.put(csum,map.get(csum)-1);
        return count;
    }
    public int pathSum(TreeNode root, int ts) {
        HashMap<Long,Integer> map = new HashMap<>();
        map.put(0L,1);
        return func(root,ts,0,map);
    }
```
### Tree Diameter (medium)
https://leetcode.com/problems/diameter-of-binary-tree/
```java
class Solution {
    int res=0;
    public int height(TreeNode root){
        if(root==null){
            return 0;
        }
        int l=height(root.left);
        int r =height(root.right);
        res=Math.max(res,l+r);
        return 1+Math.max(l,r);
    }
    public int diameterOfBinaryTree(TreeNode root) {
        height(root);
        return res;
    }
}
```
### Path with Maximum Sum (hard)
https://leetcode.com/problems/binary-tree-maximum-path-sum/
```java
class Solution {
    public int dfs(TreeNode root, int[] msum){
        if(root==null){
            return 0;
        }
        int l=Math.max(0,dfs(root.left,msum));
        int r=Math.max(0,dfs(root.right,msum));
        msum[0]=Math.max(msum[0],l+r+root.val);
        return Math.max(l,r)+root.val;
    }
    public int maxPathSum(TreeNode root) {
        int[] maxSum=new int[1];
        maxSum[0]=Integer.MIN_VALUE;
        dfs(root,maxSum);
        return maxSum[0];
    }
}
```
