# Pattern 11: Modified Binary Search
### Order-agnostic Binary Search (easy)
https://leetcode.com/problems/binary-search/
```java
class Solution {
    public int search(int[] nums, int target) {
        int l=0;
        int r=nums.length-1;
        while(l<=r){
            int mid=(l+r)/2;
            if(nums[mid]==target){
                return mid;
            }
            else if(nums[mid]<target){
                l=mid+1;
            }
            else{
                r=mid-1;
            }
        }
        return -1;
    }
}
````
### Similar Problem
https://leetcode.com/problems/search-insert-position/
```java
class Solution {
    public int searchInsert(int[] nums, int target) {
        int l=0;
        int r=nums.length-1;
        while(l<=r){
            int mid=(l+r)/2;
            if(nums[mid]==target){
                return mid;
            }
            else if(nums[mid]<target){
                l=mid+1;
            }
            else{
                r=mid-1;
            }
        }
        return l;
    }
}
````
### Next Letter (medium)
https://leetcode.com/problems/find-smallest-letter-greater-than-target/
```java
````
### Number Range (medium)
https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/
```java
````
### Search in a Sorted Infinite Array (medium)
https://leetcode.com/problems/search-in-a-sorted-array-of-unknown-size/
```java
````
### Minimum Difference Element (medium)
https://leetcode.com/problems/minimum-absolute-difference/
```java
````
### Search in Rotated Array (medium)
https://leetcode.com/problems/search-in-rotated-sorted-array/
```java
````
### Similar Problem
https://leetcode.com/problems/search-in-rotated-sorted-array-ii/
```java
````
### Rotation Count (medium)
https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/
```java
````
### Rotation count 2
https://leetcode.com/problems/find-minimum-in-rotated-sorted-array-ii/
