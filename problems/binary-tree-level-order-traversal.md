
# 102. Binary Tree Level Order Traversal - 二叉树的层序遍历

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Tree-树-blue.svg">   <img src="https://img.shields.io/badge/Breadth First Search-广度优先搜索-blue.svg">   <img src="https://img.shields.io/badge/Binary Tree-二叉树-blue.svg">  


## Description - 题目描述

### EN:
<p>Given the <code>root</code> of a binary tree, return <em>the level order traversal of its nodes&#39; values</em>. (i.e., from left to right, level by level).</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2021/02/19/tree1.jpg" style="width: 277px; height: 302px;" />
<pre>
<strong>Input:</strong> root = [3,9,20,null,null,15,7]
<strong>Output:</strong> [[3],[9,20],[15,7]]
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre>
<strong>Input:</strong> root = [1]
<strong>Output:</strong> [[1]]
</pre>

<p><strong class="example">Example 3:</strong></p>

<pre>
<strong>Input:</strong> root = []
<strong>Output:</strong> []
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li>The number of nodes in the tree is in the range <code>[0, 2000]</code>.</li>
	<li><code>-1000 &lt;= Node.val &lt;= 1000</code></li>
</ul>


### ZH-CN:
<p>给你二叉树的根节点 <code>root</code> ，返回其节点值的 <strong>层序遍历</strong> 。 （即逐层地，从左到右访问所有节点）。</p>

<p>&nbsp;</p>

<p><strong>示例 1：</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2021/02/19/tree1.jpg" style="width: 277px; height: 302px;" />
<pre>
<strong>输入：</strong>root = [3,9,20,null,null,15,7]
<strong>输出：</strong>[[3],[9,20],[15,7]]
</pre>

<p><strong>示例 2：</strong></p>

<pre>
<strong>输入：</strong>root = [1]
<strong>输出：</strong>[[1]]
</pre>

<p><strong>示例 3：</strong></p>

<pre>
<strong>输入：</strong>root = []
<strong>输出：</strong>[]
</pre>

<p>&nbsp;</p>

<p><strong>提示：</strong></p>

<ul>
	<li>树中节点数目在范围 <code>[0, 2000]</code> 内</li>
	<li><code>-1000 &lt;= Node.val &lt;= 1000</code></li>
</ul>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/binary-tree-level-order-traversal/description/)  -  [LeetCode-CN](https://leetcode.cn/problems/binary-tree-level-order-traversal/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| typescript  | 68 ms | 44.2 MB | 2022/06/10 14:54 |

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

function levelOrder(root: TreeNode | null): number[][] {
  const result: number[][] = [];
  if (root === null) return result;
  const queue: TreeNode[] = [root];
  while (queue.length) {
    const level: number[] = [];
    const size = queue.length;
    for (let i = 0; i < size; i++) {
      const node = queue.shift();
      level.push(node!.val);
      if (node!.left) queue.push(node!.left);
      if (node!.right) queue.push(node!.right);
    }
    result.push(level);
  }
  return result;
}

```
## My Notes - 我的笔记


No notes

