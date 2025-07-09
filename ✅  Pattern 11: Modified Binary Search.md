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
class Solution {
    public char nextGreatestLetter(char[] letters, char target) {
        int n=letters.length;
        int l=0;
        int r=n-1;
        while(l<=r){
            int mid=l+(r-l)/2;
            if(letters[mid]<=target){
                l=mid+1;
            }
            else{
                r=mid-1;
             }
        }
        return letters[l%n];
    }
}
````
### Number Range (medium)
https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/
```java
class Solution {
    public int[] searchRange(int[] nums, int target) {
        int[] result = {-1, -1};
        int left = binarySearch(nums, target, true);
        int right = binarySearch(nums, target, false);
        result[0] = left;
        result[1] = right;
        return result;        
    }

    private int binarySearch(int[] nums, int target, boolean isSearchingLeft) {
        int left = 0;
        int right = nums.length - 1;
        int idx = -1;

        while (left <= right) {
            int mid = left + (right - left) / 2;
            
            if (nums[mid] > target) {
                right = mid - 1;
            } else if (nums[mid] < target) {
                left = mid + 1;
            } else {
                idx = mid;
                if (isSearchingLeft) {
                    right = mid - 1;
                } else {
                    left = mid + 1;
                }
            }
        }

        return idx;
    }

}
````
### Search in a Sorted Infinite Array (medium)
https://leetcode.com/problems/search-in-a-sorted-array-of-unknown-size/
```java
https://www.geeksforgeeks.org/dsa/find-position-element-sorted-array-infinite-numbers/
````
### Minimum Difference Element (medium)
https://leetcode.com/problems/minimum-absolute-difference/
```java

````
### Search in Rotated Array (medium)
https://leetcode.com/problems/search-in-rotated-sorted-array/
```java
class Solution {
    public int search(int[] nums, int target) {
        int l=0;
        int r=nums.length-1;
        while(l<=r){
            int mid = l+(r-l)/2;
            if(nums[mid]==target){
                return mid;
            }
            //if left part is sorted
            else if(nums[mid]>=nums[l]){
                if(nums[l]<=target && target<nums[mid]){
                    r=mid-1;
                }
                else{
                    l=mid+1;
                }
            }
            //if right part is sorted
            else{
                if(nums[mid]<=target && target <=nums[r]){
                    l=mid+1;
                }
                else{
                    r=mid-1;
                }
            }
        }
        return -1;
    }
}
````
### Similar Problem
https://leetcode.com/problems/search-in-rotated-sorted-array-ii/
```java
class Solution {
    public boolean search(int[] nums, int target) {
        int l=0;
        int r=nums.length-1;
        while(l<=r){
            int mid = l+(r-l)/2;
            if(nums[mid]==target){
                return true;
            }
            if(nums[mid]==nums[l]){
                l++;
                continue;
            }
            //if left part is sorted
            else if(nums[mid]>=nums[l]){
                if(nums[l]<=target && target<=nums[mid]){
                    r=mid-1;
                }
                else{
                    l=mid+1;
                }
            }
            //if right part is sorted
            else{
                if(nums[mid]<=target && target <=nums[r]){
                    l=mid+1;
                }
                else{
                    r=mid-1;
                }
            }
        }
        return false;
    }
}
````
### Rotation Count (medium)
https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/
```java
class Solution {
    public int findMin(int[] nums) {
        int l=0;
        int h=nums.length-1;
        while(l<h){
            int mid=l+(h-l)/2;
            if(nums[mid]<nums[h]){
                h=mid;
            }
            else if(nums[mid]>nums[h]){
                l=mid+1;
            }
        }
        return nums[h];
    }
}
````
### Rotation count 2
https://leetcode.com/problems/find-minimum-in-rotated-sorted-array-ii/
```java
class Solution {
    public int findMin(int[] nums) {
        int l=0;
        int h=nums.length-1;
        while(l<h){
            int mid=l+(h-l)/2;
            if(nums[mid]<nums[h]){
                h=mid;
            }
            else if(nums[mid]>nums[h]){
                l=mid+1;
            }
            else{
                h-=1;
            }
        }
        return nums[h];
    }
}
```
