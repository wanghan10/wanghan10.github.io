---
layout: post
#标题配置
title:  LeetCode里的一些算法题，此博客长期更新
#时间配置
date:   2019-02-26 20:01:00 +0800
#大类配置
categories: 算法
#小类配置
tag: 算法题目
---

* content
{:toc}

链表：两数相加
---------------------
给出两个非空的链表用来表示两个非负的整数。其中，它们各自的位数是按照逆序的方式存储的，并且它们的每个节点只能存储一位数字。  
如果，我们将这两个数相加起来，则会返回一个新的链表来表示它们的和。  
您可以假设除了数字 0 之外，这两个数都不会以 0 开头。  

链表定义  
=========================
```java
public class ListNode {
	int val;
	ListNode next;
	ListNode(int x) { val = x; }
}
```

代码实现
=========================
```java
class Solution {
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        //resultNode作为返回
        ListNode resultNode = new ListNode(0);
        //拷贝出一个curr，用于链表滑动
    	ListNode curr = resultNode;
    	//定义遍历时使用的中间变量
    	int add = 0;
    	//对l1和l1进行遍历，各位相加
        while(l1 != null || l2 !=null) {
        	int q1 = (l1 != null) ? l1.val:0;
        	int q2 = (l2 != null) ? l2.val:0;
        	int sum = q1+q2+add;
            add =  sum / 10;
        	curr.next = new ListNode(sum % 10);
            //滑动结果链表
        	curr = curr.next;
            //滑动被加的两个链表，先判断是否为空
            if (l1 != null)
                l1 = l1.next;
            if (l2 != null)
                l2 = l2.next;
        }
        //考虑可能存在变量完成，再进一位的情况
        if (add>0)
        	curr.next = new ListNode(1);
        return resultNode.next;
        
    }
}
```