
# 19. Remove Nth Node From End of List - 删除链表的倒数第 N 个结点

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Linked List-链表-blue.svg">   <img src="https://img.shields.io/badge/Two Pointers-双指针-blue.svg">  


## Description - 题目描述

### EN:
<p>Given the <code>head</code> of a linked list, remove the <code>n<sup>th</sup></code> node from the end of the list and return its head.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2020/10/03/remove_ex1.jpg" style="width: 542px; height: 222px;" />
<pre>
<strong>Input:</strong> head = [1,2,3,4,5], n = 2
<strong>Output:</strong> [1,2,3,5]
</pre>

<p><strong>Example 2:</strong></p>

<pre>
<strong>Input:</strong> head = [1], n = 1
<strong>Output:</strong> []
</pre>

<p><strong>Example 3:</strong></p>

<pre>
<strong>Input:</strong> head = [1,2], n = 1
<strong>Output:</strong> [1]
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li>The number of nodes in the list is <code>sz</code>.</li>
	<li><code>1 &lt;= sz &lt;= 30</code></li>
	<li><code>0 &lt;= Node.val &lt;= 100</code></li>
	<li><code>1 &lt;= n &lt;= sz</code></li>
</ul>

<p>&nbsp;</p>
<p><strong>Follow up:</strong> Could you do this in one pass?</p>


### ZH-CN:
<p>给你一个链表，删除链表的倒数第&nbsp;<code>n</code><em>&nbsp;</em>个结点，并且返回链表的头结点。</p>

<p>&nbsp;</p>

<p><strong>示例 1：</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2020/10/03/remove_ex1.jpg" style="width: 542px; height: 222px;" />
<pre>
<strong>输入：</strong>head = [1,2,3,4,5], n = 2
<strong>输出：</strong>[1,2,3,5]
</pre>

<p><strong>示例 2：</strong></p>

<pre>
<strong>输入：</strong>head = [1], n = 1
<strong>输出：</strong>[]
</pre>

<p><strong>示例 3：</strong></p>

<pre>
<strong>输入：</strong>head = [1,2], n = 1
<strong>输出：</strong>[1]
</pre>

<p>&nbsp;</p>

<p><strong>提示：</strong></p>

<ul>
	<li>链表中结点的数目为 <code>sz</code></li>
	<li><code>1 &lt;= sz &lt;= 30</code></li>
	<li><code>0 &lt;= Node.val &lt;= 100</code></li>
	<li><code>1 &lt;= n &lt;= sz</code></li>
</ul>

<p>&nbsp;</p>

<p><strong>进阶：</strong>你能尝试使用一趟扫描实现吗？</p>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/remove-nth-node-from-end-of-list/description/)  -  [LeetCode-CN](https://leetcode-cn.com/problems/remove-nth-node-from-end-of-list/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| typescript  | 60 ms | 44 MB | 2022/05/02 0:11 |

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

function removeNthFromEnd(head: ListNode | null, n: number): ListNode | null {
  if (!head) {
    return head;
  }

  if (head.next === null && n === 1) {
    head = null;
    return head;
  }

  let listLen = 1;

  let cur : ListNode | null = head;

  let pre: ListNode | null = null;

  while (cur.next) {
    listLen += 1;
    cur = cur.next;
  }

  let count = listLen - n;

  cur = head;

  if (count === 1) {
    pre = head;
  }

  if (count === 0) {
    const res = head.next;

    head.next = null;

    head = null;

    return res;
  }

  for (; count > 1; count--) {
    cur = cur.next;
  }

  pre = cur;

  cur = pre.next;

  pre.next = cur.next;

  cur = null;

  return head;

};

```
## My Notes - 我的笔记


最开始的思路：先遍历一遍链表获得长度，再走 `链表长度 - n` 步得到待删除节点。

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

function removeNthFromEnd(head: ListNode | null, n: number): ListNode | null {
  if (!head) {
    return head;
  }

  if (head.next === null && n === 1) {
    head = null;
    return head;
  }

  let listLen = 1;

  let cur : ListNode | null = head;

  let pre: ListNode | null = null;

  while (cur.next) {
    listLen += 1;
    cur = cur.next;
  }

  let count = listLen - n;

  cur = head;

  if (count === 1) {
    pre = head;
  }

  if (count === 0) {
    const res = head.next;

    head.next = null;
 
    head = null;

    return res;
  }

  for (; count > 1; count--) {
    cur = cur.next;
  }

  pre = cur;

  cur = pre.next;

  pre.next = cur.next;

  cur = null;

  return head;

};
```

后来想了想，可以用快慢指针：快指针先走 n 步，ok 后慢指针和快指针同时走。当快指针走完链表时，慢指针所处位置是待删除节点的前驱。

