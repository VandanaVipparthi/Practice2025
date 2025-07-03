# Pattern 4 : Merge Intervals
### Merge Intervals
https://leetcode.com/problems/merge-intervals/description/
````java
class Solution {
    public int[][] merge(int[][] intervals) {
        Arrays.sort(intervals, (a, b) -> Integer.compare(a[0], b[0]));
        List<int[]> res = new ArrayList<>();
        res.add(intervals[0]);
        for(int i=1;i<intervals.length;i++){
            int[] last = res.get(res.size() - 1);
            if(last[1]>=intervals[i][0]){
                last[1]=Math.max(intervals[i][1],last[1]);
            }
            else{
                res.add(intervals[i]);
            }
        }
        return res.toArray(new int[res.size()][]);

    }
}
````
Time complexity: O(nlogn)
Space complexity: O(n)
### Insert Interval
https://leetcode.com/problems/insert-interval/
```java
class Solution {
    public int[][] insert(int[][] arr, int[] n) {
        List<int[]> ans= new ArrayList<>(Arrays.asList(arr));
        ans.add(n);
        Collections.sort(ans, (a, b) -> Integer.compare(a[0], b[0]));
        List<int[]> res = new ArrayList<>();
        res.add(ans.get(0));
        for(int i=1;i<ans.size();i++){
             int[] last = res.get(res.size()-1);
            if(last[1]>=ans.get(i)[0]){
                last[1]=Math.max(ans.get(i)[1],last[1]);
            }
            else{
                res.add(ans.get(i));
            }
        }
        return res.toArray(new int[res.size()][]);
    }
}
```
Time complexity: O(nlogn)
Space complexity: O(n)
### Conflicting Appointments (medium)
The problem follows the Merge Intervals pattern. We can sort all the intervals by startTime and then check if any two intervals overlap. A person will not be able to attend all appointments if any two appointments overlap.
similar pattern as above

### Meeting Rooms II
https://www.geeksforgeeks.org/problems/attend-all-meetings-ii/1
```java
class Solution {
    public int minMeetingRooms(int[] start, int[] end) {
        // code here
        Arrays.sort(start);
        Arrays.sort(end);
        int count =1;
        int maxi =1;
        int i=1,j=0;
        int n = start.length;
        while(i<n && j<n){
            if(start[i]<end[j]){
                count++;
                i++;
            }else{
                count--;
                j++;
            }
            maxi = Math.max(maxi,count);
        }
        return maxi;
    }
}
```
Time complexity: O(nlogn)
Space complexity: O(n)
### Car Pooling
https://leetcode.com/problems/car-pooling/description/
```java
class Solution {
    public boolean carPooling(int[][] trips, int capacity) {
         Map<Integer,Integer> m = new TreeMap<>();
         for(int[] t: trips){
            m.put(t[1],m.getOrDefault(t[1], 0) + t[0]);
            m.put(t[2], m.getOrDefault(t[2], 0) - t[0]);
         }
         for(int val:m.values()){
            capacity-=val;
            if(capacity<0){
                return false;
            }
         }
        return true;
    }
}
```
Time complexity: O(nlogn)
Space complexity: O(n)
