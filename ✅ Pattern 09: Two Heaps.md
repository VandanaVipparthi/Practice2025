# Pattern 9: Two Heaps
### Find the Median of a Number Stream (medium)
https://leetcode.com/problems/find-median-from-data-stream/
```
In order to always have access to the median of the dataset, we can have a left maxHeap (stores numbers left of the median) and a right minHeap (stores numbers right of the median).
In order for this to work, when inserting numbers we need to make sure that the size of the left and right Queues are equal AND left.peek() is less than right.peek() because it should be in sorted order.
```
```java
class MedianFinder {
    private PriorityQueue<Integer> left = new PriorityQueue<>((a, b) -> b - a);
    private PriorityQueue<Integer> right = new PriorityQueue<>();
    public MedianFinder() {
        
    }
    
    public void addNum(int num) {
        if (right.isEmpty() && left.isEmpty())
            left.offer(num);
        else if (right.isEmpty())
            if (left.peek() > num)
                left.offer(num);
            else
                right.offer(num);
        else if (right.peek() > num)
            left.offer(num);
        else
            right.offer(num);
        if (right.size() == left.size() + 2)
            left.offer(right.poll());
        if (right.size() + 2 == left.size())
            right.offer(left.poll());
    }
    
    public double findMedian() {
        if (left.size() == right.size())
            return (((double) right.peek() + left.peek()) / 2);
        return right.size() > left.size() ? (double) right.peek() : (double) left.peek();
    }
}
```
```
Complexity
Time complexity:
AddNum(): O(logn) - This is the complexity to insert or extract from a Queue.
findMedian(): O(1) - We only peek from the Queue, which is O(1)

Space complexity:
AddNum(): O(n) - we store as many numbers as are inserted.
findMedian(): O(1) - No need to store new data structures, only peeking.
```
### Sliding Window Median (hard)
https://leetcode.com/problems/sliding-window-median/
```java

```
### Maximize Capital (hard)
https://leetcode.com/problems/ipo/
```java

```
### Next Interval (hard)
https://leetcode.com/problems/find-right-interval/
```java

```
