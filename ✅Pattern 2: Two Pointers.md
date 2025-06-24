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
### 4. Squaring a Sorted Array (easy)
https://leetcode.com/problems/squares-of-a-sorted-array/
```
Since the original array is not sorted, it's not guaranteed that the largest elements (in terms of absolute value) are at the ends of the array.
By iterating backwards from the end of the array, we can start populating the result array from the end, ensuring that the squares of larger elements occupy the higher indices of the result array.
```
````java
public int[] sortedSquares(int[] nums) {
        int[] res = new int[nums.length];
        int l=0,r=nums.length-1;
        for(int i=nums.length-1;i>=0;i--){
            if(Math.abs(nums[l])>Math.abs(nums[r])){
                res[i]=nums[l]*nums[l];
                l++;
            }
            else{
                res[i]=nums[r]*nums[r];
                r--;
            }
        }
        return res;
    }
````
Time Complexity: O(n)
Space Complexity: O(n)

### 5. Triplet Sum to Zero (medium)
https://leetcode.com/problems/3sum/description/
```
Sort the array to handle duplicates easily and apply the two-pointer method. Loop through the array using index i (fixing one number).
For each i, use two pointers:left = i + 1, right = n - 1, to find pairs such that nums[i] + nums[left] + nums[right] == 0.
Skip duplicates for i, left, and right while moving pointers. Add valid triplets to the result list.
```
````java
public List<List<Integer>> threeSum(int[] nums) {
        Arrays.sort(nums);
        List<List<Integer>> res = new ArrayList<>();

        for (int i = 0; i < nums.length; i++) {
            if (i > 0 && nums[i] == nums[i - 1]) continue;

            int j = i + 1, k = nums.length - 1;

            while (j < k) {
                int sum = nums[i] + nums[j] + nums[k];

                if (sum < 0) j++;
                else if (sum > 0) k--;
                else {
                    res.add(Arrays.asList(nums[i], nums[j], nums[k]));
                    j++; k--;

                    while (j < k && nums[j] == nums[j - 1]) j++;
                }
            }
        }

        return res;
    }
````
Time Complexity: O(n2)
Space Complexity: O(1) (excluding output list)

### 6. 3Sum Closest
https://leetcode.com/problems/3sum-closest/description/
````
Sort the input array to simplify pointer movements. Loop over the array with index i, fixing one number. Use two pointers left and right to try all combinations with nums[i]. For every triplet, calculate the absolute difference from the target. If the current sum is closer, update the result. Move pointers inward depending on how current_sum compares to target.
````
````java
public int threeSumClosest(int[] nums, int target) {
        int minDiff =Integer.MAX_VALUE;
        Arrays.sort(nums);
        int sum=0,diff=0,s=0,m=0,e=0;
        int n=nums.length;
        for(int i=0;i<n;i++){
            int j=i+1, k=n-1;
            while(k>j){
                sum = nums[i]+nums[j]+nums[k];
                diff=Math.abs(sum-target);
                
                if(diff<minDiff){
                    minDiff=Math.abs(Math.abs(sum)-Math.abs(target));
                    s=i;
                    m=j;
                    e=k;
                }
                if(sum<target){
                    j++;
                }
                else{
                    k--;
                }
            }
        }
        return nums[s]+nums[m]+nums[e];
    }
````
Time Complexity:( O(n²) ) — outer loop + two-pointer scan
Space Complexity:( O(1) ) — constant space

### 7. Triplets with Smaller Sum (medium)
https://www.geeksforgeeks.org/problems/count-triplets-with-sum-smaller-than-x5549/1
Similar to above approach
````java
long countTriplets(int n, int sum1, long arr[]) {
        long ans=0,sum=0;
        Arrays.sort(arr);
        for(int i=0;i<n-1;i++){
            int j=i+1,k=n-1;
            while(j<k){
                sum= arr[i]+arr[j]+arr[k];
                if(sum<sum1){
                    ans+=k-j;
                    j++;
                }else{
                    k--;
                }
            }
        }
        return ans;
    }
````
Time Complexity:( O(n²) ) — outer loop + two-pointer scan
Space Complexity:( O(1) ) — constant space
### 8. Subarrays with Product Less than a Target (medium)
https://leetcode.com/problems/subarray-product-less-than-k/description/
