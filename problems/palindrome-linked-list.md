
# 234. Palindrome Linked List - 回文链表

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Stack-栈-blue.svg">   <img src="https://img.shields.io/badge/Recursion-递归-blue.svg">   <img src="https://img.shields.io/badge/Linked List-链表-blue.svg">   <img src="https://img.shields.io/badge/Two Pointers-双指针-blue.svg">  


## Description - 题目描述

### EN:
<p>Given the <code>head</code> of a singly linked list, return <code>true</code><em> if it is a </em><span data-keyword="palindrome-sequence"><em>palindrome</em></span><em> or </em><code>false</code><em> otherwise</em>.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2021/03/03/pal1linked-list.jpg" style="width: 422px; height: 62px;" />
<pre>
<strong>Input:</strong> head = [1,2,2,1]
<strong>Output:</strong> true
</pre>

<p><strong class="example">Example 2:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2021/03/03/pal2linked-list.jpg" style="width: 182px; height: 62px;" />
<pre>
<strong>Input:</strong> head = [1,2]
<strong>Output:</strong> false
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li>The number of nodes in the list is in the range <code>[1, 10<sup>5</sup>]</code>.</li>
	<li><code>0 &lt;= Node.val &lt;= 9</code></li>
</ul>

<p>&nbsp;</p>
<strong>Follow up:</strong> Could you do it in <code>O(n)</code> time and <code>O(1)</code> space?

### ZH-CN:
<p>给你一个单链表的头节点 <code>head</code> ，请你判断该链表是否为回文链表。如果是，返回 <code>true</code> ；否则，返回 <code>false</code> 。</p>

<p>&nbsp;</p>

<p><strong>示例 1：</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2021/03/03/pal1linked-list.jpg" style="width: 422px; height: 62px;" />
<pre>
<strong>输入：</strong>head = [1,2,2,1]
<strong>输出：</strong>true
</pre>

<p><strong>示例 2：</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2021/03/03/pal2linked-list.jpg" style="width: 182px; height: 62px;" />
<pre>
<strong>输入：</strong>head = [1,2]
<strong>输出：</strong>false
</pre>

<p>&nbsp;</p>

<p><strong>提示：</strong></p>

<ul>
	<li>链表中节点数目在范围<code>[1, 10<sup>5</sup>]</code> 内</li>
	<li><code>0 &lt;= Node.val &lt;= 9</code></li>
</ul>

<p>&nbsp;</p>

<p><strong>进阶：</strong>你能否用&nbsp;<code>O(n)</code> 时间复杂度和 <code>O(1)</code> 空间复杂度解决此题？</p>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/palindrome-linked-list/description/)  -  [LeetCode-CN](https://leetcode.cn/problems/palindrome-linked-list/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| typescript  | 144 ms | 62.2 MB | 2023/03/25 19:37 |

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

function isPalindrome(head: ListNode | null): boolean {

  if (head === null) {
    return false;
  }

  if (head.next === null) {
    return true;
  }

  const findMidNode = (head: ListNode | null) => {
    if (!head) {
      return null;
    }
    let fast = head, slow = head;
    while (fast !== null) {
      if (fast.next && fast.next.next) {
        fast = fast.next.next;
      } else {
        fast = null;
      }
      slow = slow.next;
    }

    return slow;
  }


  const convertLinkList = (head: ListNode | null) => {
    if (head === null) {
      return null;
    }

    let cur = head, next = head.next, temp = head.next;

    cur.next = null;

    while (next !== null) {
      temp = next;
      next = next.next;
      temp.next = cur;
      cur = temp;
    }

    return cur;

  }

  const mid = findMidNode(head);


  // convert the half link list on the back

  const tail = convertLinkList(mid);

  let front = head, back = tail;

  while (front && back) {
    if (front.val !== back.val) {
      return false;
    }
    front = front.next;
    back = back.next;
  }

  return true;
};

```
## My Notes - 我的笔记


使用 O(n) 时间复杂度和 O(1) 空间复杂度解决此题：
1. 获取链表的中间节点：快慢指针；
2. 将中间节点之后的节点所组成的链表反转，形成前半部分的链表和后半部分反转后的链表；
3. 遍历这两个链表，若遍历的每个值完全相同则原链表为回文链表。

注意：反转链表最后一步为` cur = temp`

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

function isPalindrome(head: ListNode | null): boolean {

  if (head === null) {
    return false;
  }

  if (head.next === null) {
    return true;
  }

  const findMidNode = (head: ListNode | null) => {
    if (!head) {
      return null;
    }
    let fast = head, slow = head;
    while (fast !== null) {
      if (fast.next && fast.next.next) {
        fast = fast.next.next;
      } else {
        fast = null;
      }
      slow = slow.next;
    }

    return slow;
  }


  const convertLinkList = (head: ListNode | null) => {
    if (head === null) {
      return null;
    }

    let cur = head, next = head.next, temp = head.next;

    cur.next = null;

    while (next !== null) {
      temp = next;
      next = next.next;
      temp.next = cur;
      cur = temp;
    }

    return cur;

  }

  const mid = findMidNode(head);


  // convert the half link list on the back

  const tail = convertLinkList(mid);

  let front = head, back = tail;

  while (front && back) {
    if (front.val !== back.val) {
      return false;
    }
    front = front.next;
    back = back.next;
  }

  return true;
};
```

