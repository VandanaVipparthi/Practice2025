# Pattern 5: Cyclic Sort
### Missing Number
https://leetcode.com/problems/missing-number/
```java
class Solution {
    public int missingNumber(int[] nums) {
        int xor1=0,xor2=0;
        for(int i=1;i<=nums.length;i++){
            xor1=xor1^i;
        }
        for(int j=0;j<nums.length;j++){
            xor2=xor2^nums[j];
        }
        return xor1^xor2;
    }
}
```
### Find All Numbers Disappeared in an Array
https://leetcode.com/problems/find-all-numbers-disappeared-in-an-array/description/
```java
class Solution {
    static void swap(int nums[],int s,int e){
        int temp=nums[s];
        nums[s]=nums[e];
        nums[e]=temp;
    }
    public List<Integer> findDisappearedNumbers(int[] nums) {
        int i=0;
        while(i<nums.length){
            if(nums[i]!=nums[nums[i]-1]){
                swap(nums,i,nums[i]-1);  
            }
            else{
                i++;
            }
        }
        List<Integer> ans = new ArrayList<>();
        for(int j=0;j<nums.length;j++){
            if(nums[j]!=j+1){
                ans.add(j+1);
            }
        }
        return ans;
        
    }
}
```
### Find the Duplicate Number (easy)
https://leetcode.com/problems/find-the-duplicate-number/
```java
class Solution {
    static void swap(int[] arr, int s, int e){
        int temp=arr[s];
        arr[s]=arr[e];
        arr[e]=temp;
    }
    public int findDuplicate(int[] nums) {
        int i=0;
        while(i<nums.length){
            if(nums[i] != i + 1){
                if(nums[i]!=nums[nums[i]-1]){
                swap(nums,i,nums[i]-1);
            }else{
                return nums[i];
            }
            }
            else{
                i++;
            }
        }
        
        return -1;
    }
}
```
```java
class Solution {
    public int findDuplicate(int[] nums) {
        int slow=0;
        int fast=0;
        while (true){
            slow=nums[slow];
            fast=nums[nums[fast]];
            if(slow==fast){
                break;
            }
        }
        int s=0;
        while(true){
            slow=nums[slow];
            s=nums[s];
            if(s==slow){
                return slow;
            }
        }
    }
}
```
The time complexity of the above algorithm is O(n).
The algorithm runs in constant space O(1) but modifies the input array.
### Find All Duplicates in an Array
https://leetcode.com/problems/find-all-duplicates-in-an-array/
```java
class Solution {
    static void swap(int[] arr, int s, int e){
        int temp=arr[s];
        arr[s]=arr[e];
        arr[e]=temp;
    }
    public List<Integer> findDuplicates(int[] nums) {
        ArrayList <Integer> arr= new ArrayList<>();

        int i=0;
        while(i < nums.length){
            if(nums[i] != nums[nums[i]-1]){
                swap(nums,i,nums[i]-1);
            }else{
                i++;
            }
        } 
        //store the duplicates in the list which are on the position of mising numbers
        for(int j=0;j<nums.length;j++){
            if(j != nums[j]-1){
                arr.add(nums[j]);
            }
        }
        return arr;
    }
}
```
The time complexity of the above algorithm is O(n).
### Find the Corrupt Pair (easy)
https://www.designgurus.io/course-play/grokking-the-coding-interview/doc/problem-challenge-1-find-the-corrupt-pair-easy
```java
class Solution {
    static void swap(int[] arr, int s, int e){
        int temp=arr[s];
        arr[s]=arr[e];
        arr[e]=temp;
    }
    public List<Integer> findDuplicates(int[] nums) {
        ArrayList <Integer> arr= new ArrayList<>();

        int i=0;
        while(i < nums.length){
            if(nums[i] != nums[nums[i]-1]){
                swap(nums,i,nums[i]-1);
            }else{
                i++;
            }
        } 
        //store the duplicates in the list which are on the position of mising numbers
        for(int j=0;j<nums.length;j++){
            if(j+1 != nums[j]){
                arr.add(nums[j],j+1);
            }
        }
        return arr;
    }
}
```
The time complexity of the above algorithm is O(n).
### First Missing Positive
https://leetcode.com/problems/first-missing-positive/description/
```java 
class Solution {
    static void swap(int[] arr, int s, int e){
        int temp=arr[s];
        arr[s]=arr[e];
        arr[e]=temp;
    }
    public int firstMissingPositive(int[] nums) {
        int i=0;
        while(i<nums.length){
            if(nums[i]<=0 || nums[i]>nums.length){
                i++;
            }
            else if(nums[i]!=nums[nums[i]-1]){
                swap(nums,i,nums[i]-1);
            }
            else{
                i++;
            }
        }
        for(int j=0;j<nums.length;j++){
            if(j+1!=nums[j]){return j+1;}
        }
        return i+1;
    }
}
```
### Find the First K Missing Positive Numbers (hard)
https://leetcode.com/problems/kth-missing-positive-number/
````java
class Solution {
    public int findKthPositive(int[] arr, int k) {
        int l=0,h=arr.length-1;
        while(l<=h){
            int m=(l+h)/2;
            if(arr[m]-(m+1)<k){
                l=m+1;
            }
            else{
                h=m-1;
            }
        }
        return k+h+1;
    }
}
````
Time complexity: O(log n), where n is the length of arr. This is because each step of the binary search cuts the search space in half.
Space complexity: O(1), as we only use a few variables (left, right, mid) to perform the search.
