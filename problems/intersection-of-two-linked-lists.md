
# 160. Intersection of Two Linked Lists - 相交链表

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Hash Table-哈希表-blue.svg">   <img src="https://img.shields.io/badge/Linked List-链表-blue.svg">   <img src="https://img.shields.io/badge/Two Pointers-双指针-blue.svg">  


## Description - 题目描述

### EN:
<p>Given the heads of two singly linked-lists <code>headA</code> and <code>headB</code>, return <em>the node at which the two lists intersect</em>. If the two linked lists have no intersection at all, return <code>null</code>.</p>

<p>For example, the following two linked lists begin to intersect at node <code>c1</code>:</p>
<img alt="" src="https://assets.leetcode.com/uploads/2021/03/05/160_statement.png" style="width: 500px; height: 162px;" />
<p>The test cases are generated such that there are no cycles anywhere in the entire linked structure.</p>

<p><strong>Note</strong> that the linked lists must <strong>retain their original structure</strong> after the function returns.</p>

<p><strong>Custom Judge:</strong></p>

<p>The inputs to the <strong>judge</strong> are given as follows (your program is <strong>not</strong> given these inputs):</p>

<ul>
	<li><code>intersectVal</code> - The value of the node where the intersection occurs. This is <code>0</code> if there is no intersected node.</li>
	<li><code>listA</code> - The first linked list.</li>
	<li><code>listB</code> - The second linked list.</li>
	<li><code>skipA</code> - The number of nodes to skip ahead in <code>listA</code> (starting from the head) to get to the intersected node.</li>
	<li><code>skipB</code> - The number of nodes to skip ahead in <code>listB</code> (starting from the head) to get to the intersected node.</li>
</ul>

<p>The judge will then create the linked structure based on these inputs and pass the two heads, <code>headA</code> and <code>headB</code> to your program. If you correctly return the intersected node, then your solution will be <strong>accepted</strong>.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2021/03/05/160_example_1_1.png" style="width: 500px; height: 162px;" />
<pre>
<strong>Input:</strong> intersectVal = 8, listA = [4,1,8,4,5], listB = [5,6,1,8,4,5], skipA = 2, skipB = 3
<strong>Output:</strong> Intersected at &#39;8&#39;
<strong>Explanation:</strong> The intersected node&#39;s value is 8 (note that this must not be 0 if the two lists intersect).
From the head of A, it reads as [4,1,8,4,5]. From the head of B, it reads as [5,6,1,8,4,5]. There are 2 nodes before the intersected node in A; There are 3 nodes before the intersected node in B.
- Note that the intersected node&#39;s value is not 1 because the nodes with value 1 in A and B (2<sup>nd</sup> node in A and 3<sup>rd</sup> node in B) are different node references. In other words, they point to two different locations in memory, while the nodes with value 8 in A and B (3<sup>rd</sup> node in A and 4<sup>th</sup> node in B) point to the same location in memory.
</pre>

<p><strong class="example">Example 2:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2021/03/05/160_example_2.png" style="width: 500px; height: 194px;" />
<pre>
<strong>Input:</strong> intersectVal = 2, listA = [1,9,1,2,4], listB = [3,2,4], skipA = 3, skipB = 1
<strong>Output:</strong> Intersected at &#39;2&#39;
<strong>Explanation:</strong> The intersected node&#39;s value is 2 (note that this must not be 0 if the two lists intersect).
From the head of A, it reads as [1,9,1,2,4]. From the head of B, it reads as [3,2,4]. There are 3 nodes before the intersected node in A; There are 1 node before the intersected node in B.
</pre>

<p><strong class="example">Example 3:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2021/03/05/160_example_3.png" style="width: 300px; height: 189px;" />
<pre>
<strong>Input:</strong> intersectVal = 0, listA = [2,6,4], listB = [1,5], skipA = 3, skipB = 2
<strong>Output:</strong> No intersection
<strong>Explanation:</strong> From the head of A, it reads as [2,6,4]. From the head of B, it reads as [1,5]. Since the two lists do not intersect, intersectVal must be 0, while skipA and skipB can be arbitrary values.
Explanation: The two lists do not intersect, so return null.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li>The number of nodes of <code>listA</code> is in the <code>m</code>.</li>
	<li>The number of nodes of <code>listB</code> is in the <code>n</code>.</li>
	<li><code>1 &lt;= m, n &lt;= 3 * 10<sup>4</sup></code></li>
	<li><code>1 &lt;= Node.val &lt;= 10<sup>5</sup></code></li>
	<li><code>0 &lt;= skipA &lt;&nbsp;m</code></li>
	<li><code>0 &lt;= skipB &lt;&nbsp;n</code></li>
	<li><code>intersectVal</code> is <code>0</code> if <code>listA</code> and <code>listB</code> do not intersect.</li>
	<li><code>intersectVal == listA[skipA] == listB[skipB]</code> if <code>listA</code> and <code>listB</code> intersect.</li>
</ul>

<p>&nbsp;</p>
<strong>Follow up:</strong> Could you write a solution that runs in <code>O(m + n)</code> time and use only <code>O(1)</code> memory?

### ZH-CN:
<p>给你两个单链表的头节点&nbsp;<code>headA</code> 和 <code>headB</code> ，请你找出并返回两个单链表相交的起始节点。如果两个链表不存在相交节点，返回 <code>null</code> 。</p>

<p>图示两个链表在节点 <code>c1</code> 开始相交<strong>：</strong></p>

<p><a href="https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2018/12/14/160_statement.png" target="_blank"><img alt="" src="https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2018/12/14/160_statement.png" style="height:130px; width:400px" /></a></p>

<p>题目数据 <strong>保证</strong> 整个链式结构中不存在环。</p>

<p><strong>注意</strong>，函数返回结果后，链表必须 <strong>保持其原始结构</strong> 。</p>

<p><strong>自定义评测：</strong></p>

<p><strong>评测系统</strong> 的输入如下（你设计的程序 <strong>不适用</strong> 此输入）：</p>

<ul>
	<li><code>intersectVal</code> - 相交的起始节点的值。如果不存在相交节点，这一值为 <code>0</code></li>
	<li><code>listA</code> - 第一个链表</li>
	<li><code>listB</code> - 第二个链表</li>
	<li><code>skipA</code> - 在 <code>listA</code> 中（从头节点开始）跳到交叉节点的节点数</li>
	<li><code>skipB</code> - 在 <code>listB</code> 中（从头节点开始）跳到交叉节点的节点数</li>
</ul>

<p>评测系统将根据这些输入创建链式数据结构，并将两个头节点 <code>headA</code> 和 <code>headB</code> 传递给你的程序。如果程序能够正确返回相交节点，那么你的解决方案将被 <strong>视作正确答案</strong> 。</p>

<p>&nbsp;</p>

<p><strong>示例 1：</strong></p>

<p><a href="https://assets.leetcode.com/uploads/2018/12/13/160_example_1.png" target="_blank"><img alt="" src="https://assets.leetcode.com/uploads/2021/03/05/160_example_1_1.png" style="height:130px; width:400px" /></a></p>

<pre>
<strong>输入：</strong>intersectVal = 8, listA = [4,1,8,4,5], listB = [5,6,1,8,4,5], skipA = 2, skipB = 3
<strong>输出：</strong>Intersected at '8'
<strong>解释：</strong>相交节点的值为 8 （注意，如果两个链表相交则不能为 0）。
从各自的表头开始算起，链表 A 为 [4,1,8,4,5]，链表 B 为 [5,6,1,8,4,5]。
在 A 中，相交节点前有 2 个节点；在 B 中，相交节点前有 3 个节点。
— 请注意相交节点的值不为 1，因为在链表 A 和链表 B 之中值为 1 的节点 (A 中第二个节点和 B 中第三个节点) 是不同的节点。换句话说，它们在内存中指向两个不同的位置，而链表 A 和链表 B 中值为 8 的节点 (A 中<font size="1">第三个</font>节点，B 中第四个节点) 在内存中指向相同的位置。
</pre>

<p>&nbsp;</p>

<p><strong>示例&nbsp;2：</strong></p>

<p><a href="https://assets.leetcode.com/uploads/2018/12/13/160_example_2.png" target="_blank"><img alt="" src="https://assets.leetcode.com/uploads/2021/03/05/160_example_2.png" style="height:136px; width:350px" /></a></p>

<pre>
<strong>输入：</strong>intersectVal&nbsp;= 2, listA = [1,9,1,2,4], listB = [3,2,4], skipA = 3, skipB = 1
<strong>输出：</strong>Intersected at '2'
<strong>解释：</strong>相交节点的值为 2 （注意，如果两个链表相交则不能为 0）。
从各自的表头开始算起，链表 A 为 [1,9,1,2,4]，链表 B 为 [3,2,4]。
在 A 中，相交节点前有 3 个节点；在 B 中，相交节点前有 1 个节点。
</pre>

<p><strong>示例&nbsp;3：</strong></p>

<p><a href="https://assets.leetcode.com/uploads/2018/12/13/160_example_3.png" target="_blank"><img alt="" src="https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2018/12/14/160_example_3.png" style="height:126px; width:200px" /></a></p>

<pre>
<strong>输入：</strong>intersectVal = 0, listA = [2,6,4], listB = [1,5], skipA = 3, skipB = 2
<strong>输出：</strong>null
<strong>解释：</strong>从各自的表头开始算起，链表 A 为 [2,6,4]，链表 B 为 [1,5]。
由于这两个链表不相交，所以 intersectVal 必须为 0，而 skipA 和 skipB 可以是任意值。
这两个链表不相交，因此返回 null 。
</pre>

<p>&nbsp;</p>

<p><strong>提示：</strong></p>

<ul>
	<li><code>listA</code> 中节点数目为 <code>m</code></li>
	<li><code>listB</code> 中节点数目为 <code>n</code></li>
	<li><code>1 &lt;= m, n &lt;= 3 * 10<sup>4</sup></code></li>
	<li><code>1 &lt;= Node.val &lt;= 10<sup>5</sup></code></li>
	<li><code>0 &lt;= skipA &lt;= m</code></li>
	<li><code>0 &lt;= skipB &lt;= n</code></li>
	<li>如果 <code>listA</code> 和 <code>listB</code> 没有交点，<code>intersectVal</code> 为 <code>0</code></li>
	<li>如果 <code>listA</code> 和 <code>listB</code> 有交点，<code>intersectVal == listA[skipA] == listB[skipB]</code></li>
</ul>

<p>&nbsp;</p>

<p><strong>进阶：</strong>你能否设计一个时间复杂度 <code>O(m + n)</code> 、仅用 <code>O(1)</code> 内存的解决方案？</p>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/intersection-of-two-linked-lists/description/)  -  [LeetCode-CN](https://leetcode.cn/problems/intersection-of-two-linked-lists/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| typescript  | 112 ms | 48.9 MB | 2023/03/04 22:36 |

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

function getIntersectionNode(headA: ListNode | null, headB: ListNode | null): ListNode | null {
  if (!headA || !headB) {
    return null;
  }
  // get the length of the two links
  let aLen = 1, bLen = 1;
  let curA = headA, curB = headB;
  for (; curA !== null; curA = curA.next) {
    aLen++;
  }
  for (; curB !== null; curB = curB.next) {
    bLen++;
  }

  const diff = aLen - bLen;

  curA = headA, curB = headB;

  if (diff >= 0) {
    for (let i = 0; i < diff; i++) {
      curA = curA.next;
    }
  } else {
    for (let i = 0; i < -diff; i++) {
      curB = curB.next;
    }
  }

  while (curA !== null && curB !== null) {
    if (curA === curB) {
      return curA;
    }
    curA = curA.next;
    curB = curB.next;
  }

  return null;
};

```
## My Notes - 我的笔记


思路：先拿到两个链表的长度，作差之后，长的链表先走差值，短的链表再走，最后一起走，判断交点即可。
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

function getIntersectionNode(headA: ListNode | null, headB: ListNode | null): ListNode | null {
  if (!headA || !headB) {
    return null;
  }
  // get the length of the two links
  let aLen = 1, bLen = 1;
  let curA = headA, curB = headB;
  for (; curA !== null; curA = curA.next) {
    aLen++;
  }
  for (; curB !== null; curB = curB.next) {
    bLen++;
  }

  const diff = aLen - bLen;

  curA = headA, curB = headB;

  if (diff >= 0) {
    for (let i = 0; i < diff; i++) {
      curA = curA.next;
    }
  } else {
    for (let i = 0; i < -diff; i++) {
      curB = curB.next;
    }
  }

  while (curA !== null && curB !== null) {
    if (curA === curB) {
      return curA;
    }
    curA = curA.next;
    curB = curB.next;
  }

  return null;
};
```

