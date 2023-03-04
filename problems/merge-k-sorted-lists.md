
# 23. Merge k Sorted Lists - 合并K个升序链表

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Linked List-链表-blue.svg">   <img src="https://img.shields.io/badge/Divide and Conquer-分治-blue.svg">   <img src="https://img.shields.io/badge/Heap (Priority Queue)-堆（优先队列）-blue.svg">   <img src="https://img.shields.io/badge/Merge Sort-归并排序-blue.svg">  


## Description - 题目描述

### EN:
<p>You are given an array of <code>k</code> linked-lists <code>lists</code>, each linked-list is sorted in ascending order.</p>

<p><em>Merge all the linked-lists into one sorted linked-list and return it.</em></p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input:</strong> lists = [[1,4,5],[1,3,4],[2,6]]
<strong>Output:</strong> [1,1,2,3,4,4,5,6]
<strong>Explanation:</strong> The linked-lists are:
[
  1-&gt;4-&gt;5,
  1-&gt;3-&gt;4,
  2-&gt;6
]
merging them into one sorted list:
1-&gt;1-&gt;2-&gt;3-&gt;4-&gt;4-&gt;5-&gt;6
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre>
<strong>Input:</strong> lists = []
<strong>Output:</strong> []
</pre>

<p><strong class="example">Example 3:</strong></p>

<pre>
<strong>Input:</strong> lists = [[]]
<strong>Output:</strong> []
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>k == lists.length</code></li>
	<li><code>0 &lt;= k &lt;= 10<sup>4</sup></code></li>
	<li><code>0 &lt;= lists[i].length &lt;= 500</code></li>
	<li><code>-10<sup>4</sup> &lt;= lists[i][j] &lt;= 10<sup>4</sup></code></li>
	<li><code>lists[i]</code> is sorted in <strong>ascending order</strong>.</li>
	<li>The sum of <code>lists[i].length</code> will not exceed <code>10<sup>4</sup></code>.</li>
</ul>


### ZH-CN:
<p>给你一个链表数组，每个链表都已经按升序排列。</p>

<p>请你将所有链表合并到一个升序链表中，返回合并后的链表。</p>

<p>&nbsp;</p>

<p><strong>示例 1：</strong></p>

<pre><strong>输入：</strong>lists = [[1,4,5],[1,3,4],[2,6]]
<strong>输出：</strong>[1,1,2,3,4,4,5,6]
<strong>解释：</strong>链表数组如下：
[
  1-&gt;4-&gt;5,
  1-&gt;3-&gt;4,
  2-&gt;6
]
将它们合并到一个有序链表中得到。
1-&gt;1-&gt;2-&gt;3-&gt;4-&gt;4-&gt;5-&gt;6
</pre>

<p><strong>示例 2：</strong></p>

<pre><strong>输入：</strong>lists = []
<strong>输出：</strong>[]
</pre>

<p><strong>示例 3：</strong></p>

<pre><strong>输入：</strong>lists = [[]]
<strong>输出：</strong>[]
</pre>

<p>&nbsp;</p>

<p><strong>提示：</strong></p>

<ul>
	<li><code>k == lists.length</code></li>
	<li><code>0 &lt;= k &lt;= 10^4</code></li>
	<li><code>0 &lt;= lists[i].length &lt;= 500</code></li>
	<li><code>-10^4 &lt;= lists[i][j] &lt;= 10^4</code></li>
	<li><code>lists[i]</code> 按 <strong>升序</strong> 排列</li>
	<li><code>lists[i].length</code> 的总和不超过 <code>10^4</code></li>
</ul>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/merge-k-sorted-lists/description/)  -  [LeetCode-CN](https://leetcode.cn/problems/merge-k-sorted-lists/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| typescript  | 216 ms | 46.8 MB | 2022/05/03 15:41 |

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

function mergeKLists(lists: Array<ListNode | null>): ListNode | null {
  return lists.reduce((acc, cur) => {
    return mergeTwoList(acc, cur);
  }, null);
};

function mergeTwoList(list1: ListNode | null, list2: ListNode | null): ListNode | null {
  if (!list1) {
    return list2 ?? null;
  }

  if (!list2) {
    return list1 ?? null;
  }

  let p1 = list1, p2 = list2;

  let fakeHead: ListNode | null = new ListNode();

  let cur = fakeHead;

  while (p1 && p2) {
    if (p1.val < p2.val) {
      cur.next = p1;
      p1 = p1.next;
      cur = cur.next;
      cur.next = null;
    } else {
      cur.next = p2;
      p2 = p2.next;
      cur = cur.next;
      cur.next = null;
    }
  }

  if (!p1) {
    cur.next = p2;
  }

  if (!p2) {
    cur.next = p1;
  }

  return fakeHead.next;
}

```
## My Notes - 我的笔记


逐一合并两个排序链表即可。

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

function mergeKLists(lists: Array<ListNode | null>): ListNode | null {
  return lists.reduce((acc, cur) => {
    return mergeTwoList(acc, cur);
  }, null);
};

function mergeTwoList(list1: ListNode | null, list2: ListNode | null): ListNode | null {
  if (!list1) {
    return list2 ?? null;
  }

  if (!list2) {
    return list1 ?? null;
  }

  let p1 = list1, p2 = list2;

  let fakeHead: ListNode | null = new ListNode();

  let cur = fakeHead;

  while (p1 && p2) {
    if (p1.val < p2.val) {
      cur.next = p1;
      p1 = p1.next;
      cur = cur.next;
      cur.next = null;
    } else {
      cur.next = p2;
      p2 = p2.next;
      cur = cur.next;
      cur.next = null;
    }
  }

  if (!p1) {
    cur.next = p2;
  }

  if (!p2) {
    cur.next = p1;
  }

  return fakeHead.next;
}
```

合并的链表，既可以 new 一个新的节点，也可以复用原来链表的节点。new 一个新结点的代码如下：

```typescript
    if (p1.val < p2.val) {
      cur.next = new ListNode(p1.val);
      p1 = p1.next;
      cur = cur.next;
    } else {
      cur.next = new ListNode(p2.val);
      p2 = p2.next;
      cur = cur.next;
    }
```

其他思路：遍历所有链表的当前节点，用优先队列做。


