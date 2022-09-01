
# 剑指 Offer 24. 反转链表 LCOF - 反转链表

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Recursion-递归-blue.svg">   <img src="https://img.shields.io/badge/Linked List-链表-blue.svg">  


## Description - 题目描述

### EN:
<p>English description is not available for the problem. Please switch to Chinese.</p>


### ZH-CN:
<p>定义一个函数，输入一个链表的头节点，反转该链表并输出反转后链表的头节点。</p>

<p>&nbsp;</p>

<p><strong>示例:</strong></p>

<pre><strong>输入:</strong> 1-&gt;2-&gt;3-&gt;4-&gt;5-&gt;NULL
<strong>输出:</strong> 5-&gt;4-&gt;3-&gt;2-&gt;1-&gt;NULL</pre>

<p>&nbsp;</p>

<p><strong>限制：</strong></p>

<p><code>0 &lt;= 节点个数 &lt;= 5000</code></p>

<p>&nbsp;</p>

<p><strong>注意</strong>：本题与主站 206 题相同：<a href="https://leetcode-cn.com/problems/reverse-linked-list/">https://leetcode-cn.com/problems/reverse-linked-list/</a></p>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/fan-zhuan-lian-biao-lcof/description/)  -  [LeetCode-CN](https://leetcode.cn/problems/fan-zhuan-lian-biao-lcof/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| typescript  | 80 ms | 39.8 MB | 2021/11/04 16:13 |

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

function reverseList(head: ListNode | null): ListNode | null {
  if (!head) {
    return null;
  }

  let prev = null, cur = head, next = cur?.next ?? null;

  while (cur) {
    next = cur.next; // 相当于一个 temp 变量，保存原链表 cur 的下一个指针
    cur.next = prev;

    //  while 循环，自增变量一般最后再考虑
    prev = cur;
    cur = next;
  }
  return prev; // cur 为 null 时，prev 为原链表的尾
};

```
## My Notes - 我的笔记


1. 自己的解法
```typescript
function reverseList(head: ListNode | null): ListNode | null {
  if (!head) {
    return null;
  }
  let cur = head, prev = null, next = cur?.next ?? null;

  while (next) {
    if (prev?.next === cur) {
      prev.next = null;
    }
    prev = cur;
    cur = next;
    next = cur.next;
    cur.next = prev;
  }
  if (prev?.next === cur) {
    prev.next = null;
  }
  return cur;
};
```

2. 官方解法
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

function reverseList(head: ListNode | null): ListNode | null {
  if (!head) {
    return null;
  }

  let prev = null, cur = head, next = cur?.next ?? null;

  while (cur) {
    next = cur.next; // 相当于一个 temp 变量，保存原链表 cur 的下一个指针
    cur.next = prev;

    // while 循环，自增变量一般最后再考虑
    prev = cur;
    cur = next;
  }
  return prev; // cur 为 null 时，prev 为原链表的尾
};
```

