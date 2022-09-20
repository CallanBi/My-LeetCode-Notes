
# 148. Sort List - 排序链表

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Linked List-链表-blue.svg">   <img src="https://img.shields.io/badge/Two Pointers-双指针-blue.svg">   <img src="https://img.shields.io/badge/Divide and Conquer-分治-blue.svg">   <img src="https://img.shields.io/badge/Sorting-排序-blue.svg">   <img src="https://img.shields.io/badge/Merge Sort-归并排序-blue.svg">  


## Description - 题目描述

### EN:
<p>Given the <code>head</code> of a linked list, return <em>the list after sorting it in <strong>ascending order</strong></em>.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2020/09/14/sort_list_1.jpg" style="width: 450px; height: 194px;" />
<pre>
<strong>Input:</strong> head = [4,2,1,3]
<strong>Output:</strong> [1,2,3,4]
</pre>

<p><strong>Example 2:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2020/09/14/sort_list_2.jpg" style="width: 550px; height: 184px;" />
<pre>
<strong>Input:</strong> head = [-1,5,3,4,0]
<strong>Output:</strong> [-1,0,3,4,5]
</pre>

<p><strong>Example 3:</strong></p>

<pre>
<strong>Input:</strong> head = []
<strong>Output:</strong> []
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li>The number of nodes in the list is in the range <code>[0, 5 * 10<sup>4</sup>]</code>.</li>
	<li><code>-10<sup>5</sup> &lt;= Node.val &lt;= 10<sup>5</sup></code></li>
</ul>

<p>&nbsp;</p>
<p><strong>Follow up:</strong> Can you sort the linked list in <code>O(n logn)</code> time and <code>O(1)</code> memory (i.e. constant space)?</p>


### ZH-CN:
<p>给你链表的头结点&nbsp;<code>head</code>&nbsp;，请将其按 <strong>升序</strong> 排列并返回 <strong>排序后的链表</strong> 。</p>

<ul>
</ul>

<p>&nbsp;</p>

<p><strong>示例 1：</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2020/09/14/sort_list_1.jpg" style="width: 450px;" />
<pre>
<b>输入：</b>head = [4,2,1,3]
<b>输出：</b>[1,2,3,4]
</pre>

<p><strong>示例 2：</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2020/09/14/sort_list_2.jpg" style="width: 550px;" />
<pre>
<b>输入：</b>head = [-1,5,3,4,0]
<b>输出：</b>[-1,0,3,4,5]
</pre>

<p><strong>示例 3：</strong></p>

<pre>
<b>输入：</b>head = []
<b>输出：</b>[]
</pre>

<p>&nbsp;</p>

<p><b>提示：</b></p>

<ul>
	<li>链表中节点的数目在范围&nbsp;<code>[0, 5 * 10<sup>4</sup>]</code>&nbsp;内</li>
	<li><code>-10<sup>5</sup>&nbsp;&lt;= Node.val &lt;= 10<sup>5</sup></code></li>
</ul>

<p>&nbsp;</p>

<p><b>进阶：</b>你可以在&nbsp;<code>O(n&nbsp;log&nbsp;n)</code> 时间复杂度和常数级空间复杂度下，对链表进行排序吗？</p>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/sort-list/description/)  -  [LeetCode-CN](https://leetcode.cn/problems/sort-list/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| typescript  | 188 ms | 66.9 MB | 2022/09/20 21:36 |

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
function merge(l1: ListNode, l2: ListNode): ListNode {
  let dummyHead = new ListNode();

  let temp = dummyHead, cur1 = l1, cur2 = l2;

  while (cur1 && cur2) {
    if (cur1.val <= cur2.val) {
      temp.next = cur1;
      cur1 = cur1.next;
    } else {
      temp.next = cur2;
      cur2 = cur2.next;
    }
    temp = temp.next;
  }

  if (cur1) {
    temp.next = cur1;
  } else if (cur2) {
    temp.next = cur2;
  }

  return dummyHead.next;
}


function sort(head: ListNode | null, tail: ListNode | null): ListNode {
  if (head === null) {
    return head;
  }

  if (head.next === tail) {
    head.next = null;
    return head;
  }

  let slow = head, fast = head;

  while (fast && fast !== tail) {
    slow = slow.next;
    fast = fast.next;
    if (fast && fast !== tail) {
      fast = fast.next;
    }
  }

  const mid = slow;
  return merge(sort(head, mid), sort(mid, tail));
}

function sortList(head: ListNode | null): ListNode | null {
  return sort(head, null)
};

```
## My Notes - 我的笔记


使用归并排序排序链表。

链表不同于顺序表，需要选用适合的的排序方法，可以参考：[排序链表「八大排序算法」](https://leetcode.cn/problems/sort-list/solution/by-itcharge-01zg/)。

下面用归并排序实现。

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
function merge(l1: ListNode, l2: ListNode): ListNode {
  let dummyHead = new ListNode();

  let temp = dummyHead, cur1 = l1, cur2 = l2;

  while (cur1 && cur2) {
    if (cur1.val <= cur2.val) {
      temp.next = cur1;
      cur1 = cur1.next;
    } else {
      temp.next = cur2;
      cur2 = cur2.next;
    }
    temp = temp.next;
  }

  if (cur1) {
    temp.next = cur1;
  } else if (cur2) {
    temp.next = cur2;
  }

  return dummyHead.next;
}


function sort(head: ListNode | null, tail: ListNode | null): ListNode {
  if (head === null) {
    return head;
  }

  if (head.next === tail) {
    head.next = null;
    return head;
  }

  let slow = head, fast = head;

  while (fast && fast !== tail) {
    slow = slow.next;
    fast = fast.next;
    if (fast && fast !== tail) {
      fast = fast.next;
    }
  }

  const mid = slow;
  return merge(sort(head, mid), sort(mid, tail));
}

function sortList(head: ListNode | null): ListNode | null {
  return sort(head, null)
};
```

注意：合并两个有序链表中，判断结尾的条件不是 `fast === null`，而是`fast === tail`，因为我们是选用了是否到达尾部节点作为递归终止条件。


