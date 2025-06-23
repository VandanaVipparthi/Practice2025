# Pattern 2: Two Pointers
### 1.Pair with Target Sum aka "Two Sum" (easy)
https://leetcode.com/problems/two-sum/description/

<b> Optimized Approach </b>
````java
i) store all the elements and its indexes in hashmap.
ii) find if map contains target-nums[r] and if yes then retrieve the index from map and check if its != r then return r and the index you retreive from the map.
````
````java
public int[] twoSum(int[] nums, int target) {
        int[] ans = new int[2];
        HashMap<Integer,Integer> map = new HashMap<>();
        for(int i=0;i<nums.length;i++){
            map.put(nums[i],i);
        }
        
        for(int r=0;r<nums.length;r++){
                if(map.containsKey(target-nums[r]) && map.get(target-nums[r])!=r){
    
                    return new int[]{r,map.get(target-nums[r])};
                }
        }
        return ans;
    }
````
Time Complexity: O(n)
Space Complexity: O(1)
### 2. Remove Duplicates from Sorted Array
https://leetcode.com/problems/remove-duplicates-from-sorted-array/description/

<b> Optimized Approach </b>
````java
public int removeDuplicates(int[] nums) {
       int n=nums.length,l=0,r=1;
       while(r<n && l<n){
        if(nums[l]==nums[r]){
            r++;
        }
        else{
            l++;
            int temp=nums[l];
            nums[l]=nums[r];
            nums[r]=temp;
            r++;
        }
       }
       return l+1; 
    }
````
Time Complexity: O(n)
Space Complexity: O(1)

### 3. Remove Element
https://leetcode.com/problems/remove-element/description/

````java
Initialize index to 0, which represents the current position for the next non-target element.
Iterate through each element of the input array using the i pointer.
For each element nums[i], check if it is equal to the target value.
If nums[i] is not equal to val, it means it is a non-target element.
Set nums[index] to nums[i] to store the non-target element at the current index position.
Increment index by 1 to move to the next position for the next non-target element.
Continue this process until all elements in the array have been processed.
Finally, return the value of index, which represents the length of the modified array.
````
<b> Optimized Approach </b>
````java
public int removeElement(int[] nums, int val) {
        int index=0;
        for(int i=0;i<nums.length;i++){
            if(nums[i]!=val){
                nums[index]=nums[i];
                index++;
            }
        }
        return index;
    }
````
Time Complexity: O(n)
Space Complexity: O(1)
