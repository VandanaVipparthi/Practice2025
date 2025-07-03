# Pattern 6: In-place Reversal of a LinkedList.md
### Reverse a LinkedList (easy)
https://leetcode.com/problems/reverse-linked-list/
```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public ListNode reverseList(ListNode head) {
        ListNode prev=null;
        ListNode curr=head;
        while(curr!=null){
            ListNode temp=curr.next;
            curr.next=prev;
            prev=curr;
            curr=temp;
        }
        return prev;
    }
}
```
Time complexity: O(n)
Space complexity: O(1)

### Reverse a Sub-list (medium)
https://leetcode.com/problems/reverse-linked-list-ii/
```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public ListNode reverseBetween(ListNode head, int left, int right) {
         if (head == null || left == right) {
            return head;
        }
        ListNode dummy = new ListNode(0);
        dummy.next = head;
        ListNode lprev=dummy;
        ListNode curr=head;
        for(int i=0;i<left-1;i++){
            lprev=curr;
            curr=curr.next;
        }
        ListNode prev=null;
        for(int i=0;i<right-left+1;i++){
            ListNode temp=curr.next;
            curr.next=prev;
            prev=curr;
            curr=temp;
        }
        lprev.next.next=curr;
        lprev.next=prev;
        
        return dummy.next;
    }
}
```
Time 𝑂(𝑛)
Space 𝑂(1)

### Reverse every K-element Sub-list (medium)
https://leetcode.com/problems/reverse-nodes-in-k-group/
```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public ListNode reverse(ListNode head){
        ListNode prev=null;
        ListNode curr=head;
        while(curr!=null){
            ListNode temp=curr.next;
            curr.next=prev;
            prev=curr;
            curr=temp;
        }
        return prev;
    }
    public ListNode findKthNode(ListNode temp, int k){
        k-=1;
        while(temp!=null && k>0){
            temp=temp.next;
            k--;
        }
        return temp;
    }
    public ListNode reverseKGroup(ListNode head, int k) {
        ListNode temp = head;
        ListNode prev = null;
        while(temp!=null){
            ListNode kthNode = findKthNode(temp,k);
            if(kthNode==null){
                if(prev!=null){
                    prev.next=temp;
                }
                break;
            }
            ListNode nn = kthNode.next;
            kthNode.next=null;
            reverse(temp);
            if(temp==head){
                head=kthNode;
            }
            else{
                prev.next=kthNode;
            }
            prev=temp;
            temp=nn;
        }
        return head;
    }
}
```

### Rotate a LinkedList (medium)
https://leetcode.com/problems/rotate-list/
```java
class Solution {
    public ListNode rotateRight(ListNode head, int k) {
        int length=1;
        if (head == null) return head;
        ListNode temp=head;
        while(temp.next!=null){
            temp=temp.next;
            length++;
        }
        int position = k % length;
        if (position == 0) return head;
        ListNode curr=head;
        for(int i=0;i<length-1-position;i++){
            curr=curr.next;
        }
        ListNode newHead=curr.next;
        curr.next=null;
        temp.next=head;
        return newHead;
    }
}
```
