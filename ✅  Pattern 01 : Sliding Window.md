## Pattern 1: Sliding Window
The sliding window technique is used to efficiently process a contiguous section of data (like a substring or subarray) while avoiding unnecesary recomputation.
### Find Averages of Sub Arrays
https://leetcode.com/problems/maximum-average-subarray-i/
````java
Input: nums = [1,12,-5,-6,50,3], k = 4
Output: 12.75000
Explanation: Maximum average is (12 - 5 - 6 + 50) / 4 = 51 / 4 = 12.75
````
<b>Brute Force Approach</b>
This algorithm will find all the sum of k contiguous arrays and then find the average. 
Time Complexity: O(N*K)
Space Complexity: O(1)
````java
double findAvgOfSubArrays(int[] nums, int k){
  double ans=Double.MIN_VALUE;
        for(int i=0;i<nums.length-k+1;i++){
            double sum=0;
            for(int j=i;j<i+k;j++){
            sum+=nums[j];
            }
            ans=Math.max(ans,sum/k);
        }
        return ans;
}
````
Inneficiency: The inefficiency is that for any two consecutive subarrays of size `k`, the overlapping part (which will contain k-1 elements) will be evaluated twice.
<b> Optimized Approach </b>
In this approach first we will calculate the sum of first K elements and store the value. Then slide the window by one element while sliding add the rightmost element in window and remove the leftmost element in the array. 
````java

double findAvgOfSubArrays(int[] nums, int k){
  double sum=0;
  for(int i=0;i<k;i++){
    sum+=nums[i];
  }
  double maxSum =sum;
  for(int i=k; i<nums.length;i++){
    sum+=nums[i]-nums[i-k];
    maxSum=Math.max(maxSum,sum);
  }
  return maxSum/k;
}
````
Time Complexity: O(N)
Space Complexity: O(1)
