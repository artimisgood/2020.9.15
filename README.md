# 2020.9.15每日算法题————两数相加
## 题目
给出两个 非空 的链表用来表示两个非负的整数。其中，它们各自的位数是按照 逆序 的方式存储的，并且它们的每个节点只能存储 一位 数字。

如果，我们将这两个数相加起来，则会返回一个新的链表来表示它们的和。

您可以假设除了数字 0 之外，这两个数都不会以 0 开头。

示例：

输入：(2 -> 4 -> 3) + (5 -> 6 -> 4)
输出：7 -> 0 -> 8
原因：342 + 465 = 807

## 解题
### 语言 java
### 思路 
![](https://pic.leetcode-cn.com/2519bd7f7da0f3bd51dd0f06e6363f4f62bfb25472c5ec233cf969e5c1472e33-file_1559748028103)
![](https://pic.leetcode-cn.com/400f2a615319c4f0f42c39eb8b8902984922d1e778ca461569ff64460eaa9757-file_1559748028117)
![](https://pic.leetcode-cn.com/e0d3266ec83cee00c6a0ff0a8a66de8d129798b24b76a19b7883f2fd1d79c15b-file_1559748087173)
![](https://pic.leetcode-cn.com/a5bf6bc2cc15d162bd35eb8fc467fb36887e40b36c26bdc982a11a686b34cb30-file_1559748028113)
![](https://pic.leetcode-cn.com/fc6475aca0ec0621003f4888a59086c398ff5fc6ee2e27cbfb9bc91f107383b9-file_1559748028094)
![](https://pic.leetcode-cn.com/743afc3cb34954e1f3a9b41924d4af5453832d23772a2e46aa4cd52a2b240bdd-file_1559748028108)
![](https://pic.leetcode-cn.com/3323b948431675b9f2ff8b0161eee9178298cbb4403cbcd36dc857f14043cf7a-file_1559748028112)
![](https://pic.leetcode-cn.com/508d1bb12a372e385c4052d95ca92e06c3a63a805bf12feddd0bb4e7c972f016-file_1559748028116)
将两个链表看成是相同长度的进行遍历，如果一个链表较短则在前面补 00，比如 987 + 23 = 987 + 023 = 1010。每一位计算的同时需要考虑上一位的进位问题，而当前位计算结束后同样需要更新进位值。如果两个链表全部遍历完毕后，进位值为 11，则在新链表最前方添加节点 11。小技巧：对于链表问题，返回结果为头结点时，通常需要先初始化一个预先指针 pre，该指针的下一个节点指向真正的头结点head。使用预先指针的目的在于链表初始化时无可用节点值，而且链表构造过程需要指针移动，进而会导致头指针丢失，无法返回结果。
### 代码
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
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        ListNode pre = new ListNode(0);//新建一个结果链表
        ListNode cur = pre;
        int carry = 0;//设置进位为零
        while(l1!=null||l2!=null){
            int x = l1==null?0:l1.val;
            int y = l2==null?0:l2.val;
            int sum = x+y+carry;

            carry = sum/10;//计算进位数
            sum = sum%10;//计算此位是多少
            cur.next = new ListNode(sum);

            cur = cur.next;
            if(l1!=null)//进行遍历
                l1=l1.next;
            if(l2!=null)
                l2=l2.next;
        }
        if(carry==1){//如果多了一位
            cur.next = new ListNode(carry);
        }
        return pre.next;
    }
}
```
