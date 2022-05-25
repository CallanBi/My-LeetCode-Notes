
# 剑指 Offer 25. 合并两个排序的链表  LCOF - 合并两个排序的链表

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Recursion-递归-blue.svg">   <img src="https://img.shields.io/badge/Linked List-链表-blue.svg">  


## Description - 题目描述

### EN:
English description is not available for the problem. Please switch to Chinese.

### ZH-CN:
<p>输入两个递增排序的链表，合并这两个链表并使新链表中的节点仍然是递增排序的。</p>

<p><strong>示例1：</strong></p>

<pre><strong>输入：</strong>1-&gt;2-&gt;4, 1-&gt;3-&gt;4
<strong>输出：</strong>1-&gt;1-&gt;2-&gt;3-&gt;4-&gt;4</pre>

<p><strong>限制：</strong></p>

<p><code>0 &lt;= 链表长度 &lt;= 1000</code></p>

<p>注意：本题与主站 21 题相同：<a href="https://leetcode-cn.com/problems/merge-two-sorted-lists/">https://leetcode-cn.com/problems/merge-two-sorted-lists/</a></p>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/he-bing-liang-ge-pai-xu-de-lian-biao-lcof/description/)  -  [LeetCode-CN](https://leetcode.cn/problems/he-bing-liang-ge-pai-xu-de-lian-biao-lcof/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| typescript  | 88 ms | 42.9 MB | 2021/11/05 14:34 |

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

function mergeTwoLists(l1: ListNode | null, l2: ListNode | null): ListNode | null {
  if (!l1 && !l2) {
    return null;
  } else if (!l1 || !l2) {
    return !l1 ? l2 : l1;
  }

  const fakeHead = new ListNode();
  let i = l1, j = l2, cur = fakeHead, temp = null;
  while (i && j) {
    if (i.val <= j.val) {
      temp = i.next;
      cur.next = i;
      cur = i;
      i = temp;
    } else {
      temp = j.next;
      cur.next = j;
      cur = j;
      j = temp;
    }
  }

  if (!i && j) {
    cur.next = j;
  } else if (i && !j) {
    cur.next = i;
  }

  return fakeHead.next;
};

```
## My Notes - 我的笔记


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

function mergeTwoLists(l1: ListNode | null, l2: ListNode | null): ListNode | null {
  if (!l1 && !l2) {
    return null;
  } else if (!l1 || !l2) {
    return !l1 ? l2 : l1;
  }

  const fakeHead = new ListNode();
  let i = l1, j = l2, cur = fakeHead, temp = null; // fakeHead 作为哨兵，返回合并的链表头部
  while (i && j) {
    if (i.val <= j.val) {
      temp = i.next;
      cur.next = i;
      cur = i; // 注意 cur.next = i, cur = i, i = temp 的顺序
      i = temp;
    } else {
      temp = j.next;
      cur.next = j;
      cur = j;
      j = temp;
    }
  }

  if (!i && j) {
    cur.next = j;
  } else if (i && !j) {
    cur.next = i;
  }

  return fakeHead.next;
};
```

