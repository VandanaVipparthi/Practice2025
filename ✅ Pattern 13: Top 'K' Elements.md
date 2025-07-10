# Pattern 13: Top 'K' Elements
### Kth Smallest Number (easy)
https://leetcode.com/problems/kth-largest-element-in-an-array/
```java
public int findKthLargest(int[] nums, int k) {
        PriorityQueue<Integer> pq=new PriorityQueue<>((a,b)->Integer.compare(b,a));
        for(int i: nums) pq.add(i);
        for(int i=0;i<k-1;i++){
            pq.poll();
        }
        return pq.poll();

    }
````
### 'K' Closest Points to the Origin (easy)
https://leetcode.com/problems/k-closest-points-to-origin/
```java
class Solution {
    public int[][] kClosest(int[][] points, int k) {
        PriorityQueue<int[]> q1= new PriorityQueue<>((q,p)->(p[0]*p[0]+p[1]*p[1])-(q[0]*q[0]+q[1]*q[1]));
        for(int i=0;i<points.length;i++){
            q1.add(points[i]);
            if (q1.size() > k) {
            q1.poll();
        }
        }
        int[][] res = new int[k][2];
        while(k>0){
            res[--k] = q1.poll();
        }
        return res;
    }
}
```
### Connect Ropes (easy)
https://leetcode.com/problems/minimum-cost-to-connect-sticks/
````java
public static int minCost(int[] arr) {
        // code here
        int totalCost =0;
        PriorityQueue<Integer> minHeap = new PriorityQueue<>();
        int n = arr.length;
        for(int i =0;i<n;i++)
        {
            minHeap.add(arr[i]);
        }
        
        while(minHeap.size() >= 2)
        {
            
            int rope1 = minHeap.poll();
            int rope2 = minHeap.poll();
            
            totalCost = totalCost + rope1 + rope2;
            
            minHeap.add(rope1+rope2);
        }
        
        return totalCost;
    }
````
### Top 'K' Frequent Numbers (medium)
https://leetcode.com/problems/top-k-frequent-elements/
```java
class Solution {
    public int[] topKFrequent(int[] nums, int k) {
        HashMap<Integer,Integer> map = new HashMap<>();
        for(int i=0;i<nums.length;i++){
            map.put(nums[i],map.getOrDefault(nums[i],0)+1);
        }
        PriorityQueue<Integer> q= new PriorityQueue<>((a,b)->map.getOrDefault(a,0)-map.getOrDefault(b,0));
        for(int value: map.keySet()){
            q.add(value);
            if(q.size()>k){
                q.poll();
            }
        }
        int[] ans = new int[k];
        for (int i = 0; i < k; i++)
            ans[i] = q.poll();

        return ans;

    }
}
```
### Frequency Sort (medium)
https://leetcode.com/problems/sort-characters-by-frequency/
```java
class Solution {
    public String frequencySort(String s) {
        Map<Character,Integer> map = new HashMap<>();
        for(int i=0;i<s.length();i++){
            char c=s.charAt(i);
            map.put(c,map.getOrDefault(c,0)+1);
        }
        PriorityQueue<Map.Entry<Character, Integer>> heap=new PriorityQueue<>((a,b)->b.getValue()-a.getValue());
        
        heap.addAll(map.entrySet());

        StringBuilder result = new StringBuilder();
        while(!heap.isEmpty()){
            Map.Entry<Character,Integer> e= heap.poll();
            result.append(String.valueOf(e.getKey()).repeat(e.getValue()));
        }
        return result.toString();

    }
}
```
### Kth Largest Number in a Stream (medium)
https://leetcode.com/problems/kth-largest-element-in-a-stream/
```java
class KthLargest {
    int k;
    PriorityQueue<Integer> minHeap;
    public KthLargest(int k, int[] nums) {
        this.k = k;
        minHeap = new PriorityQueue<>();
        for(int n:nums){
            add(n);
        }
    }
    
    public int add(int val) {
        minHeap.offer(val);
        if(minHeap.size()>k) minHeap.poll();
        return minHeap.peek();
    }
}
```
### 'K' Closest Numbers (medium)
https://leetcode.com/problems/find-k-closest-elements/
```java
class Solution {
    public List<Integer> findClosestElements(int[] nums, int k, int x) {
        int left = 0, right = nums.length - 1;
        while (right - left >= k) {
            if (x - nums[left] > nums[right] - x) {
                left++;
            } else {
                right--;
            }
        }
        return Arrays.stream(nums, left, left + k)
                             .boxed()
                             .collect(Collectors.toList());
    }
}
```
### Maximum Distinct Elements (medium)
https://leetcode.com/problems/least-number-of-unique-integers-after-k-removals/
```java
class Solution {
    public int findLeastNumOfUniqueInts(int[] arr, int k) {
        Map<Integer, Integer> mp = new HashMap<>();
        for (int a : arr) mp.put(a, mp.getOrDefault(a, 0) + 1);
        PriorityQueue<int[]> q= new PriorityQueue<>((a,b)-> a[1]-b[1]);
        for(int key:mp.keySet()){
            q.offer(new int[]{key,mp.get(key)});
        }
        for(int i=0;i<k;i++){
           int a[]=q.poll();
           if(a[1]>1){
               a[1]--;
               q.offer(a);
           
            }
        }
        return q.size();
    }
}
```
### Sum of Elements (medium)
https://www.geeksforgeeks.org/sum-elements-k1th-k2th-smallest-elements/
```java
public static long sumBetweenTwoKth(long A[], long N, long K1, long K2) {
        // Your code goes here
        Arrays.sort(A);
        
        int fn = (int)K1;
        int sn = (int)K2 - 1;
        long sum = 0;
        
        for(long i=fn; i<sn; i++){
            sum += A[i];
        }
        
        return sum;
    }
```
### Rearrange String (hard)
https://leetcode.com/problems/reorganize-string/
```java
public class Solution {
    public String reorganizeString(String s) {
        HashMap<Character, Integer> freqMap = new HashMap<>();
        for (char c : s.toCharArray()) {
            freqMap.put(c, freqMap.getOrDefault(c, 0) + 1);
        }

        PriorityQueue<Character> maxHeap = new PriorityQueue<>((a, b) -> freqMap.get(b) - freqMap.get(a));
        maxHeap.addAll(freqMap.keySet());

        StringBuilder res = new StringBuilder();
        while (maxHeap.size() >= 2) {
            char char1 = maxHeap.poll();
            char char2 = maxHeap.poll();

            res.append(char1);
            res.append(char2);

            freqMap.put(char1, freqMap.get(char1) - 1);
            freqMap.put(char2, freqMap.get(char2) - 1);

            if (freqMap.get(char1) > 0) maxHeap.add(char1);
            if (freqMap.get(char2) > 0) maxHeap.add(char2);
        }

        if (!maxHeap.isEmpty()) {
            char ch = maxHeap.poll();
            if (freqMap.get(ch) > 1) return "";
            res.append(ch);
        }

        return res.toString();
    }
}
```
### Rearrange String K Distance Apart (hard)
https://leetcode.com/problems/rearrange-string-k-distance-apart/

### Scheduling Tasks (hard)
https://leetcode.com/problems/task-scheduler/

### Frequency Stack (hard)
https://leetcode.com/problems/maximum-frequency-stack/


