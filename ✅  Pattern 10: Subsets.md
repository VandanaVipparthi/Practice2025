# Pattern 10: Subsets
### Subsets (easy)
https://leetcode.com/problems/subsets/
```java
class Solution {
    public void backtracking(int[] nums,List<List<Integer>> s,List<Integer> temp, int ind){
        s.add(new ArrayList<>(temp));
        for(int i=ind;i<nums.length;i++){
            temp.add(nums[i]);
            backtracking(nums,s,temp,i+1);
            temp.remove(temp.size()-1);
        }
    }
    public List<List<Integer>> subsets(int[] nums) {
        List<List<Integer>> s = new ArrayList<>();
        backtracking(nums, s,new ArrayList<>(),0);
        return s;
    }
}
```
### Subsets With Duplicates (medium)
https://leetcode.com/problems/subsets-ii/
```java
class Solution {
     public void backtracking(int[] nums,List<List<Integer>> s,List<Integer> temp, int ind){
        s.add(new ArrayList<>(temp));
        for(int i=ind;i<nums.length;i++){
            if(i>ind && nums[i]==nums[i-1]) continue;
            temp.add(nums[i]);
            backtracking(nums,s,temp,i+1);
            temp.remove(temp.size()-1);
        }
    }
    public List<List<Integer>> subsetsWithDup(int[] nums) {
        Arrays.sort(nums);
        List<List<Integer>> s = new ArrayList<>();
        backtracking(nums, s,new ArrayList<>(),0);
        return s;
    }
}
```
### Permutations (medium)
https://leetcode.com/problems/permutations/
```java
class Solution {
    public void backtracking(int[] nums,List<List<Integer>> s,List<Integer> temp, int ind){
        if(temp.size()==nums.length){
            s.add(new ArrayList<>(temp));
        }else{
        for(int i=0;i<nums.length;i++){
            if(temp.contains(nums[i]))continue;
            temp.add(nums[i]);
            backtracking(nums,s,temp,i+1);
            temp.remove(temp.size()-1);
        }}
    }
    public List<List<Integer>> permute(int[] nums) {
       List<List<Integer>> s = new ArrayList<>();
        backtracking(nums, s,new ArrayList<>(),0);
        return s; 
    }
}
```
### String Permutations by changing case (medium)
https://leetcode.com/problems/letter-case-permutation/
```java
class Solution {
    private void backtrack(String output, String input, List<String> result) {
        if (input.isEmpty()) {
            result.add(output);
            return;
        }
        char c = input.charAt(0);
        String remaining = input.substring(1);
        if (Character.isDigit(c)) {
            backtrack(output + c, remaining, result);
        } else {
            backtrack(output + Character.toLowerCase(c), remaining, result);
            backtrack(output + Character.toUpperCase(c), remaining, result);
        }
    }
    public List<String> letterCasePermutation(String s) {
        List<String> result = new ArrayList<>();
        backtrack("", s, result);
        return result;
    }
}
```
### Balanced Parentheses (hard)
https://leetcode.com/problems/generate-parentheses/
```java
class Solution {
    public void recurse(List<String> res, int left, int right, String s, int n) {
        if (s.length() == n * 2) {
            res.add(s);
            return;
        }
        
        if (left < n) {
            recurse(res, left + 1, right, s + "(", n);
        }
        
        if (right < left) {
            recurse(res, left, right + 1, s + ")", n);
        }
    }
    public List<String> generateParenthesis(int n) {
        List<String> res = new ArrayList<String>();
        recurse(res, 0, 0, "", n);
        return res;
    }
}
```
### Unique Generalized Abbreviations (hard)
https://leetcode.com/problems/generalized-abbreviation/
```java
class Solution {
    private List<String> abbreviations;

    public List<String> generateAbbreviations(String word) {
        abbreviations = new ArrayList<>();
        dfs(word, 0, new StringBuilder(), 0);
        return abbreviations;
    }

    // pos: current position in word
    // sb: current abbreviation being built
    // count: how many characters have been abbreviated so far
    private void dfs(String word, int pos, StringBuilder sb, int count) {
        int len = sb.length(); // Save length to backtrack later

        if (pos == word.length()) {
            if (count > 0) sb.append(count); // If any pending count, add it
            abbreviations.add(sb.toString());
        } else {
            // Option 1: Abbreviate this character
            dfs(word, pos + 1, sb, count + 1);

            // Option 2: Keep this character
            if (count > 0) sb.append(count); // Add pending count before char
            sb.append(word.charAt(pos));
            dfs(word, pos + 1, sb, 0);
        }

        sb.setLength(len); // Backtrack
    }
}

```
### Evaluate Expression (hard)
https://leetcode.com/problems/different-ways-to-add-parentheses/
```java
class Solution {
    public List<Integer> diffWaysToCompute(String expression) {
        List<Integer> res = new ArrayList<>();
        for (int i = 0; i < expression.length(); ++i) {
            char oper = expression.charAt(i);
            if (oper == '+' || oper == '-' || oper == '*') {
                List<Integer> s1 = diffWaysToCompute(expression.substring(0, i));
                List<Integer> s2 = diffWaysToCompute(expression.substring(i + 1));
                for (int a : s1) {
                    for (int b : s2) {
                        if (oper == '+') res.add(a + b);
                        else if (oper == '-') res.add(a - b);
                        else if (oper == '*') res.add(a * b);
                    }
                }
            }
        }
        if (res.isEmpty()) res.add(Integer.parseInt(expression));
        return res;
    }
}
```
### Structurally Unique Binary Search Trees (hard)
https://leetcode.com/problems/unique-binary-search-trees-ii/
```java

```
### Count of Structurally Unique Binary Search Trees (hard)
https://leetcode.com/problems/unique-binary-search-trees/
```java

```
