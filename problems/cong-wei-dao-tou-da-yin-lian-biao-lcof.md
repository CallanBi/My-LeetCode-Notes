
# 剑指 Offer 06. 从尾到头打印链表 LCOF - 从尾到头打印链表

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Stack-栈-blue.svg">   <img src="https://img.shields.io/badge/Recursion-递归-blue.svg">   <img src="https://img.shields.io/badge/Linked List-链表-blue.svg">   <img src="https://img.shields.io/badge/Two Pointers-双指针-blue.svg">  


## Description - 题目描述

### EN:
<p>English description is not available for the problem. Please switch to Chinese.</p>

### ZH-CN:
<p>输入一个链表的头节点，从尾到头反过来返回每个节点的值（用数组返回）。</p>

<p>&nbsp;</p>

<p><strong>示例 1：</strong></p>

<pre><strong>输入：</strong>head = [1,3,2]
<strong>输出：</strong>[2,3,1]</pre>

<p>&nbsp;</p>

<p><strong>限制：</strong></p>

<p><code>0 &lt;= 链表长度 &lt;= 10000</code></p>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/cong-wei-dao-tou-da-yin-lian-biao-lcof/description/)  -  [LeetCode-CN](https://leetcode-cn.com/problems/cong-wei-dao-tou-da-yin-lian-biao-lcof/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| typescript  | 108 ms | 39.8 MB | 2021/04/03 23:11 |

```typescript

/**
 * Definition for singly-linked list.
 * class ListNode {
 *     val: number
 *     next: ListNode | null
 *     constructor(val?: number, next?: ListNode | null) {
 *         this.val = (val===undefined ? 0 : val)
 *         this.next = (next===undefined ? null : next)
 *     }
 * }
 */

function reversePrint(head: ListNode | null): number[] {
  const res: number[] = [];
  for (let cur = head; cur !== null; cur = cur.next ) {
    res.unshift(cur.val);
  }
  return res;
};

```
## My Notes - 我的笔记


for 循环基本知识都忘了。。。本质上是一个条件
先判断条件，条件决定的循环体执行，然后再执行 for循环的最后一句语句。

剑指 offer 思路：递归的本质就是栈

