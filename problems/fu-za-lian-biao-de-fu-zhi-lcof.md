
# 剑指 Offer 35. 复杂链表的复制  LCOF - 复杂链表的复制

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Hash Table-哈希表-blue.svg">   <img src="https://img.shields.io/badge/Linked List-链表-blue.svg">  


## Description - 题目描述

### EN:
English description is not available for the problem. Please switch to Chinese.

### ZH-CN:
<p>请实现 <code>copyRandomList</code> 函数，复制一个复杂链表。在复杂链表中，每个节点除了有一个 <code>next</code> 指针指向下一个节点，还有一个 <code>random</code> 指针指向链表中的任意节点或者 <code>null</code>。</p>

<p>&nbsp;</p>

<p><strong>示例 1：</strong></p>

<p><img alt="" src="https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2020/01/09/e1.png"></p>

<pre><strong>输入：</strong>head = [[7,null],[13,0],[11,4],[10,2],[1,0]]
<strong>输出：</strong>[[7,null],[13,0],[11,4],[10,2],[1,0]]
</pre>

<p><strong>示例 2：</strong></p>

<p><img alt="" src="https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2020/01/09/e2.png"></p>

<pre><strong>输入：</strong>head = [[1,1],[2,1]]
<strong>输出：</strong>[[1,1],[2,1]]
</pre>

<p><strong>示例 3：</strong></p>

<p><strong><img alt="" src="https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2020/01/09/e3.png"></strong></p>

<pre><strong>输入：</strong>head = [[3,null],[3,0],[3,null]]
<strong>输出：</strong>[[3,null],[3,0],[3,null]]
</pre>

<p><strong>示例 4：</strong></p>

<pre><strong>输入：</strong>head = []
<strong>输出：</strong>[]
<strong>解释：</strong>给定的链表为空（空指针），因此返回 null。
</pre>

<p>&nbsp;</p>

<p><strong>提示：</strong></p>

<ul>
	<li><code>-10000 &lt;= Node.val &lt;= 10000</code></li>
	<li><code>Node.random</code>&nbsp;为空（null）或指向链表中的节点。</li>
	<li>节点数目不超过 1000 。</li>
</ul>

<p>&nbsp;</p>

<p><strong>注意：</strong>本题与主站 138 题相同：<a href="https://leetcode-cn.com/problems/copy-list-with-random-pointer/">https://leetcode-cn.com/problems/copy-list-with-random-pointer/</a></p>

<p>&nbsp;</p>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/fu-za-lian-biao-de-fu-zhi-lcof/description/)  -  [LeetCode-CN](https://leetcode-cn.com/problems/fu-za-lian-biao-de-fu-zhi-lcof/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| javascript  | 72 ms | 39.4 MB | 2021/11/09 13:51 |

```javascript

/**
 * // Definition for a Node.
 * function Node(val, next, random) {
 *    this.val = val;
 *    this.next = next;
 *    this.random = random;
 * };
 */

/**
 * @param {Node} head
 * @return {Node}
 */
var copyRandomList = function(head) {
  if (!head) {
    return null;
  }

  const map = new Map();

  function copyNode(node) {
    if (!node) {
      return null;
    }

    const res = new Node(node.val, null, null);

    map.set(node, res);

    res.val = node.val;

    if (node.next) {
      if (map.has(node.next)) {
        res.next = map.get(node.next);
      } else {
        res.next = copyNode(node.next);
        map.set(node.next, res.next);
      }
    } else {
      res.next = null;
    }

    if (node.random) {
      if (map.has(node.random)) {
        res.random = map.get(node.random);
      } else {
        res.random = copyNode(node.random);
        map.set(node.random, res.random);
      }
    } else {
      res.random = null;
    }

    return res;
  }

  const res = copyNode(head);

  return res;
}

```
## My Notes - 我的笔记


第一遍写时的解法，哈希表+递归
```javascript
/**
 * // Definition for a Node.
 * function Node(val, next, random) {
 *    this.val = val;
 *    this.next = next;
 *    this.random = random;
 * };
 */

/**
 * @param {Node} head
 * @return {Node}
 */
var copyRandomList = function(head) {
  if (!head) {
    return null;
  }

  const map = new Map();

  function copyNode(node) {
    if (!node) {
      return null;
    }

    const res = new Node(node.val, null, null);

    map.set(node, res);

    res.val = node.val;

    if (node.next) {
      if (map.has(node.next)) {
        res.next = map.get(node.next);
      } else {
        res.next = copyNode(node.next);
        map.set(node.next, res.next);
      }
    } else {
      res.next = null;
    }

    if (node.random) {
      if (map.has(node.random)) {
        res.random = map.get(node.random);
      } else {
        res.random = copyNode(node.random);
        map.set(node.random, res.random);
      }
    } else {
      res.random = null;
    }

    return res;
  }

  const res = copyNode(head);

  return res;
}
```

