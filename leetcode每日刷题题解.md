# leetcode每日刷题题解

## 1、剑指offer 21（简单）

这道题我是用的是两次循环进行的解题。

首先便是创建一个新的数组用于充足数组，数组的大小和参数中的数组大小一致。

第一次循环将奇数存入到新的数组中。

第二次循环再将偶数存入到新的数组中。

最后便将最后的得到的新数组返回。

```java
class Solution {
    public int[] exchange(int[] nums) {
        int[] arr=new int[nums.length];
        if(nums.length==0){
            return arr;
        }

        int j=0;
        for(int i=0;i<nums.length;i++){
            if(nums[i]%2!=0){
                arr[j]=nums[i];
                j++;
            }
        }
        
        for(int i=0;i<nums.length;i++){
            if(nums[i]%2==0){
                arr[j]=nums[i];
                j++;
            }
        }
        return arr;
    }
}
```

## 2、剑指offer 22（简单）

这是一道简单链表题。

我们要返回倒数第K个结点，我们不知道链表的长度，如果循环一次，使用一个计数器计算长度，然后再次循环寻找倒数第K个结点，会白浪费时间，所以我们使用双指针使用一次循环。

我们定义两个双指针，将一个指针相对于另外一个指针提前k步。

然后使用一个while循环，当前面的指针为空时停止。

最后返回后面一个指针指向的结点即可。

```Java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    public ListNode getKthFromEnd(ListNode head, int k) {
        //双指针解题
        ListNode p1=head;
        ListNode p2=head;

        for(int i=0;i<k;i++){
            p2=p2.next;
        }

        while(p2!=null){
            p1=p1.next;
            p2=p2.next;
        }
        return p1;
    }
}
```

## 3、剑指offer 23（简单）

反转链表我们有很多种方法。

其一，我们可以借助栈的数据结构，先遍历链表将每个结点存入栈中，然后再次循环从栈中取出结点形成新的反转链表。该方法简单易理解，但是占用的时间和空间资源较多。

其二，我们可以使用双指针，通过一个while循环，每次局部反转指针的指向，即后面的结点指向前面的结点形成反转。

因为有null的存在，最后返回前面的结点即可。

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    public ListNode reverseList(ListNode head) {
        //双指针
        ListNode pre=head;
        ListNode font=null;
        
        while(pre!=null){
            ListNode temp=pre.next;
            pre.next=font;
            font=pre;
            pre=temp;
        }
        return font;
    }
}
```

## 4、剑指offer 24（简单）

合并两个递增的链表。

这个题解题思路很明确，我们可以定义一个新的节点，然后通过循环进行两个链表节点值得对比，若一个链表的节点的值小于等于另外一个节点的值，那么我们便将这个节点加入到新的链表中。

若一个链表的遍历完，而另外一个链表还没有遍历完，那么说明我们没有遍历完的链表节点的值全部大于遍历完链表节点的值，我们将其全部添加到新链表之后。

最后返回新链表的头节点即可。

```Java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
        ListNode p=new ListNode(0);
        ListNode cur=new ListNode(0);
        cur=p;
        ListNode p1=l1;
        ListNode p2=l2;
        while(p1!=null&&p2!=null){
            if(p1.val<=p2.val){
                p.next=p1;
                p1=p1.next;
                p=p.next;
            }else{
                p.next=p2;
                p2=p2.next;
                p=p.next;
            }
        }
        if(p1!=null){
            p.next=p1;
        }
        if(p2!=null){
            p.next=p2;
        }
        return cur.next;
    }
}
```

