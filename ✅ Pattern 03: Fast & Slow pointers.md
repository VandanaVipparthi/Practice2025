#Pattern 3: Fast & Slow pointers
### LinkedList Cycle (easy)
https://leetcode.com/problems/linked-list-cycle/
````java
Also known as the "hare and tortoise" algorithm, this method uses two pointers that traverse the list at different speeds. The slow pointer moves one step at a time, while the fast pointer moves two steps. If there is a cycle, the fast pointer will eventually catch up to the slow pointer.
````
````java
public boolean hasCycle(ListNode head) {
        ListNode fast=head;
        ListNode slow=head;
        while(fast!=null && fast.next!=null){
            fast=fast.next.next;
            slow=slow.next;
            if(fast==slow){
                return true;
            }
        }
        return false;
    }
````
Time Complexity: O(n) — In the worst-case scenario, each node is visited once.
Space Complexity: O(1) — Constant space is used.
### Start of LinkedList Cycle (medium)
https://leetcode.com/problems/linked-list-cycle-ii/description/
````
When the two pointers meet, we know that there is a cycle in the linked list.
We then reset the slow pointer to the head of the linked list and move both pointers at the same pace, one step at a time, until they meet again.
The node where they meet is the starting point of the cycle.
If there is no cycle in the linked list, the algorithm will return null.
````
````java
public ListNode detectCycle(ListNode head) {
        ListNode slow=head;
        ListNode fast=head;
        while(fast!=null && fast.next!=null){
            fast=fast.next.next;
            slow=slow.next;
            if(fast==slow){
                break;
            }
        }
        if(fast==null || fast.next==null) return null;
        fast=head;
        while(fast!=slow){
            fast=fast.next;
            slow=slow.next;
        }
        return slow;
    }
````
Time complexity : O(n)
Space complexity : O(1)
### Happy Number (medium)
https://leetcode.com/problems/happy-number/description/
````java
public int func(int n){
        int output=0;
        while(n>0){
            int n1=n%10;
            output+=n1*n1;
            n=n/10;
        }
        return output;
    }
    public boolean isHappy(int n) {
        HashSet<Integer> set = new HashSet<>();
        while(!set.contains(n)){
            set.add(n);
            n=func(n);
            if(n==1){
                return true;
            }
        }
        return false;
    }
````
Time complexity: O(logn)
In the isHappy function, the sum of the squares of each digit is calculated to generate the next number. Repeating this operation will eventually cause the sequence to converge within a certain range. Specifically, no matter how large the starting number is, continuously calculating the sum of the squares will always cause the sequence to converge to a single-digit or two-digit number.
Due to this convergence, the number of iterations in the while loop is bounded within a certain range. Specifically, the number of iterations until the sequence converges to a single-digit or two-digit number is limited, and this is the constant k. Therefore, the number of iterations is bounded by a constant, making the time complexity O(k).
Since O(k) is a small constant, the time complexity can be simplified from O(k∗logn) to O(logn). Here, O(logn) represents the time to calculate the sum of the squares of each digit.
Space complexity: O(k)
k is the number of unique numbers encountered and stored in the visit set before a cycle is detected or the number 1 is found.
### Middle of the LinkedList (easy)
https://leetcode.com/problems/middle-of-the-linked-list/
```
1 . Initialize Two Pointers :slow = head (moves 1 node at a time) fast = head (moves 2 nodes at a time)
2 . Traverse the List : While fast != null and fast.next != null:
▪ Move slow forward by 1 node (slow = slow.next)
▪ Move fast forward by 2 nodes (fast = fast.next.next)
3 . Termination Condition : When fast reaches the end, slow will be at the middle node.
```
```java
public ListNode middleNode(ListNode head) {
        if(head==null || head.next == null) return head;
        ListNode slow=head,fast=head;
        while(fast != null && fast.next != null){
            slow = slow.next;
            fast = fast.next.next;
        }
        return slow;
        
    }
```
Time complexity:O(n)
Space complexity:O(1)
### Palindrome LinkedList (medium)
https://leetcode.com/problems/palindrome-linked-list/

```java
public boolean isPalindrome(ListNode head) {
        List<Integer> arr = new ArrayList<>();

        while (head != null) {
            arr.add(head.val);
            head = head.next;
        }

        int left = 0;
        int right = arr.size() - 1;

        while (left < right) {
            if (!arr.get(left).equals(arr.get(right))) {
                return false;
            }
            left++;
            right--;
        }

        return true;  
    }
````
Time complexity:O(n)
Space complexity:O(n)
````java
class Solution {
    public boolean isPalindrome(ListNode head) {
        ListNode slow = head;
        ListNode fast = head;

        while (fast != null && fast.next != null) {
            fast = fast.next.next;
            slow = slow.next;
        }

        ListNode prev = null;
        while (slow != null) {
            ListNode temp = slow.next;
            slow.next = prev;
            prev = slow;
            slow = temp;
        }

        ListNode first = head;
        ListNode second = prev;

        while (second != null) {
            if (first.val != second.val) {
                return false;
            }
            first = first.next;
            second = second.next;
        }

        return true; 
    }
}
````
###Rearrange a LinkedList (medium)
https://leetcode.com/problems/reorder-list/
````java
public void reorderList(ListNode head) {
         if (head == null) return;
        ListNode slow=head;
        ListNode fast=head;
        while(fast!=null && fast.next!=null){
            slow=slow.next;
            fast=fast.next.next;
        }
        ListNode p=null;
        ListNode temp=null;
    ListNode s = slow.next;
        slow.next = null;
        while(s!=null){
            temp=s.next;
            s.next=p;
            p=s;
            s=temp;
        }
        fast=head;
        ListNode prev=p;
        while(prev!=null){
            ListNode temp1=fast.next, temp2=prev.next;
            fast.next=prev;
            prev.next=temp1;
            fast=temp1;
            prev=temp2;
        }
````
### Circular Array Loop
https://leetcode.com/problems/circular-array-loop/description/
````java
class Solution {
    public int findNextIndex(int index,int[] nums,int cd){
        int n= (index+nums[index])% nums.length;
        System.out.println(n);
        if(n<0){
            n+=nums.length;
        }
        int d=nums[n]>0?1:-1;
        if(cd!=d || index==n){
            return -1;
        }
        return n;
    }
    public boolean circularArrayLoop(int[] nums) {
        HashSet<Integer> s=new HashSet<>();
        for(int i=0;i<nums.length;i++){
            if(s.contains(i)){
                continue;
            }
            int sp=i;
            int fp=i;
            int cd = nums[i] >0 ? 1 :-1;
            while(true){
            s.add(sp);
            s.add(fp);
            sp=findNextIndex(sp,nums,cd);
            fp=findNextIndex(fp,nums,cd);
            if(sp==-1 || fp==-1){
                break; 
            }
            fp=findNextIndex(fp,nums,cd);
            if(fp==-1){
                break; 
            }
            if(sp==fp){
                return true;
            }
        }
        }
        return false;
    }
}
````
