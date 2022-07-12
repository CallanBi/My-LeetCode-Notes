
# 114. Flatten Binary Tree to Linked List - 二叉树展开为链表

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Stack-栈-blue.svg">   <img src="https://img.shields.io/badge/Tree-树-blue.svg">   <img src="https://img.shields.io/badge/Depth First Search-深度优先搜索-blue.svg">   <img src="https://img.shields.io/badge/Linked List-链表-blue.svg">   <img src="https://img.shields.io/badge/Binary Tree-二叉树-blue.svg">  


## Description - 题目描述

### EN:
<p>Given the <code>root</code> of a binary tree, flatten the tree into a &quot;linked list&quot;:</p>

<ul>
	<li>The &quot;linked list&quot; should use the same <code>TreeNode</code> class where the <code>right</code> child pointer points to the next node in the list and the <code>left</code> child pointer is always <code>null</code>.</li>
	<li>The &quot;linked list&quot; should be in the same order as a <a href="https://en.wikipedia.org/wiki/Tree_traversal#Pre-order,_NLR" target="_blank"><strong>pre-order</strong><strong> traversal</strong></a> of the binary tree.</li>
</ul>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2021/01/14/flaten.jpg" style="width: 500px; height: 226px;" />
<pre>
<strong>Input:</strong> root = [1,2,5,3,4,null,6]
<strong>Output:</strong> [1,null,2,null,3,null,4,null,5,null,6]
</pre>

<p><strong>Example 2:</strong></p>

<pre>
<strong>Input:</strong> root = []
<strong>Output:</strong> []
</pre>

<p><strong>Example 3:</strong></p>

<pre>
<strong>Input:</strong> root = [0]
<strong>Output:</strong> [0]
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li>The number of nodes in the tree is in the range <code>[0, 2000]</code>.</li>
	<li><code>-100 &lt;= Node.val &lt;= 100</code></li>
</ul>

<p>&nbsp;</p>
<strong>Follow up:</strong> Can you flatten the tree in-place (with <code>O(1)</code> extra space)?

### ZH-CN:
<p>给你二叉树的根结点 <code>root</code> ，请你将它展开为一个单链表：</p>

<ul>
	<li>展开后的单链表应该同样使用 <code>TreeNode</code> ，其中 <code>right</code> 子指针指向链表中下一个结点，而左子指针始终为 <code>null</code> 。</li>
	<li>展开后的单链表应该与二叉树 <a href="https://baike.baidu.com/item/%E5%85%88%E5%BA%8F%E9%81%8D%E5%8E%86/6442839?fr=aladdin" target="_blank"><strong>先序遍历</strong></a> 顺序相同。</li>
</ul>

<p> </p>

<p><strong>示例 1：</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2021/01/14/flaten.jpg" style="width: 500px; height: 226px;" />
<pre>
<strong>输入：</strong>root = [1,2,5,3,4,null,6]
<strong>输出：</strong>[1,null,2,null,3,null,4,null,5,null,6]
</pre>

<p><strong>示例 2：</strong></p>

<pre>
<strong>输入：</strong>root = []
<strong>输出：</strong>[]
</pre>

<p><strong>示例 3：</strong></p>

<pre>
<strong>输入：</strong>root = [0]
<strong>输出：</strong>[0]
</pre>

<p> </p>

<p><strong>提示：</strong></p>

<ul>
	<li>树中结点数在范围 <code>[0, 2000]</code> 内</li>
	<li><code>-100 <= Node.val <= 100</code></li>
</ul>

<p> </p>

<p><strong>进阶：</strong>你可以使用原地算法（<code>O(1)</code> 额外空间）展开这棵树吗？</p>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/flatten-binary-tree-to-linked-list/description/)  -  [LeetCode-CN](https://leetcode.cn/problems/flatten-binary-tree-to-linked-list/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| typescript  | 72 ms | 44.2 MB | 2022/07/11 15:47 |

```typescript

/**
 * Definition for a binary tree node.
 * class TreeNode {
 *     val: number
 *     left: TreeNode | null
 *     right: TreeNode | null
 *     constructor(val?: number, left?: TreeNode | null, right?: TreeNode | null) {
 *         this.val = (val===undefined ? 0 : val)
 *         this.left = (left===undefined ? null : left)
 *         this.right = (right===undefined ? null : right)
 *     }
 * }
 */

/**
 Do not return anything, modify root in-place instead.
 */
function flatten(root: TreeNode | null): void {
  if (!root) {
    return;
  }

  function connect(cur: TreeNode & {
    newRight?: TreeNode | null;
  } | null, parent: TreeNode & {
    newRight?: TreeNode | null;
  } | null): TreeNode | null {
    if (!cur) {
      return null;
    }
    if (parent) {
      parent.newRight = cur;
    }

    const pre = connect(cur.left, cur);
    const pre2 = connect(cur.right, pre);

    if (!pre && !pre2) {
      return cur;
    } else if (!pre && pre2) {
      return pre2;
    } else if (!pre2 && pre) {
      return pre;
    } else if (pre && pre2) {
      return pre2;
    }
  }

  function clean(cur: TreeNode & {
    newRight?: TreeNode | null;
  } | null): void {
    if (!cur) {
      return;
    }

    if (cur.newRight) {
      cur.right = cur.newRight;
      delete cur.newRight;
    }
    cur.left = null;

    clean(cur.left);
    clean(cur.right);
  }

  connect(root, null)
  clean(root);

};



```
## My Notes - 我的笔记


最开始的思路：新增一个 newRight 属性来存储已经改变过的数组，第二次再遍历树清除newRight即可。

```typescript
/**
 * Definition for a binary tree node.
 * class TreeNode {
 *     val: number
 *     left: TreeNode | null
 *     right: TreeNode | null
 *     constructor(val?: number, left?: TreeNode | null, right?: TreeNode | null) {
 *         this.val = (val===undefined ? 0 : val)
 *         this.left = (left===undefined ? null : left)
 *         this.right = (right===undefined ? null : right)
 *     }
 * }
 */

/**
 Do not return anything, modify root in-place instead.
 */
function flatten(root: TreeNode | null): void {
  if (!root) {
    return;
  }

  function connect(cur: TreeNode & {
    newRight?: TreeNode | null;
  } | null, parent: TreeNode & {
    newRight?: TreeNode | null;
  } | null): TreeNode | null {
    if (!cur) {
      return null;
    }
    if (parent) {
      parent.newRight = cur;
    }

    const pre = connect(cur.left, cur);
    const pre2 = connect(cur.right, pre);

    if (!pre && !pre2) {
      return cur;
    } else if (!pre && pre2) {
      return pre2;
    } else if (!pre2 && pre) {
      return pre;
    } else if (pre && pre2) {
      return pre2;
    }
  }

  function clean(cur: TreeNode & {
    newRight?: TreeNode | null;
  } | null): void {
    if (!cur) {
      return;
    }

    if (cur.newRight) {
      cur.right = cur.newRight;
      delete cur.newRight;
    }
    cur.left = null;

    clean(cur.left);
    clean(cur.right);
  }

  connect(root, null)
  clean(root);

};
```


