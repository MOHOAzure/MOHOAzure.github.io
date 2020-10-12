# Merge two sorted lists
```java
public class ListNode {
    int val;
    ListNode next=null;
    ListNode(int x) { val = x; }
}

class Solution {
    public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
        if(l1==null) return l2;
        if(l2==null) return l1;
        if(l1.val > l2.val){
            l2.next = mergeTwoLists(l1, l2.next); // the next two candidates are the current l1 and l2.next
            return l2;
        }
        else{
            l1.next = mergeTwoLists(l1.next, l2); // the next two candidates are the current l2 and l1.next
            return l1;
        }
    }
    
    public ListNode mergeTwoListsIter(ListNode l1, ListNode l2) {
        ListNode ptrAns = new ListNode(0); // point to the answer. The only one node which doesn't reallocate
        ListNode tmpAns = ptrAns; // temporarily record the smallest element
        
        while(l1!= null && l2!=null){
            if(l1.val>l2.val){
                tmpAns.next = l2;
                l2 = l2.next; //update the candidate of l2
            }
            else{
                tmpAns.next = l1;
                l1 = l1.next; //update the candidate of l1
            }
            tmpAns = tmpAns.next; // ready for the next smallest element
        }
        if(l1==null) tmpAns.next = l2;
        if(l2==null) tmpAns.next = l1;
        
        return ptrAns.next; //return the address where the ans starts
    }
}

class Playground {
    public static void main(String[ ] args) {
        ListNode nodeA = new ListNode(1);
        ListNode nodeB = new ListNode(2);
        ListNode nodeC = new ListNode(3);
        
        ListNode nodeX = new ListNode(2);
        ListNode nodeY = new ListNode(4);
        ListNode nodeZ = new ListNode(5);
        
        nodeA.next=nodeB;
        nodeB.next=nodeC;
        
        nodeX.next=nodeY;
        nodeY.next=nodeZ;
        
        Solution sol = new Solution();
        
        // Divide & Conquer
        ListNode nodeAnswer = sol.mergeTwoLists(nodeA, nodeX);
        
        // Dynamic Programming
        ListNode nodeAnswer = sol.mergeTwoListsIter(nodeA, nodeX);        
    }
}
```
