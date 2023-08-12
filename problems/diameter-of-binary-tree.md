
# 543. Diameter of Binary Tree - 二叉树的直径

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Tree-树-blue.svg">   <img src="https://img.shields.io/badge/Depth First Search-深度优先搜索-blue.svg">   <img src="https://img.shields.io/badge/Binary Tree-二叉树-blue.svg">  


## Description - 题目描述

### EN:
<p>Given the <code>root</code> of a binary tree, return <em>the length of the <strong>diameter</strong> of the tree</em>.</p>

<p>The <strong>diameter</strong> of a binary tree is the <strong>length</strong> of the longest path between any two nodes in a tree. This path may or may not pass through the <code>root</code>.</p>

<p>The <strong>length</strong> of a path between two nodes is represented by the number of edges between them.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2021/03/06/diamtree.jpg" style="width: 292px; height: 302px;" />
<pre>
<strong>Input:</strong> root = [1,2,3,4,5]
<strong>Output:</strong> 3
<strong>Explanation:</strong> 3 is the length of the path [4,2,1,3] or [5,2,1,3].
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre>
<strong>Input:</strong> root = [1,2]
<strong>Output:</strong> 1
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li>The number of nodes in the tree is in the range <code>[1, 10<sup>4</sup>]</code>.</li>
	<li><code>-100 &lt;= Node.val &lt;= 100</code></li>
</ul>


### ZH-CN:
<p>给你一棵二叉树的根节点，返回该树的 <strong>直径</strong> 。</p>

<p>二叉树的 <strong>直径</strong> 是指树中任意两个节点之间最长路径的 <strong>长度</strong> 。这条路径可能经过也可能不经过根节点 <code>root</code> 。</p>

<p>两节点之间路径的 <strong>长度</strong> 由它们之间边数表示。</p>

<p>&nbsp;</p>

<p><strong class="example">示例 1：</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2021/03/06/diamtree.jpg" style="width: 292px; height: 302px;" />
<pre>
<strong>输入：</strong>root = [1,2,3,4,5]
<strong>输出：</strong>3
<strong>解释：</strong>3 ，取路径 [4,2,1,3] 或 [5,2,1,3] 的长度。
</pre>

<p><strong class="example">示例 2：</strong></p>

<pre>
<strong>输入：</strong>root = [1,2]
<strong>输出：</strong>1
</pre>

<p>&nbsp;</p>

<p><strong>提示：</strong></p>

<ul>
	<li>树中节点数目在范围 <code>[1, 10<sup>4</sup>]</code> 内</li>
	<li><code>-100 &lt;= Node.val &lt;= 100</code></li>
</ul>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/diameter-of-binary-tree/description/)  -  [LeetCode-CN](https://leetcode.cn/problems/diameter-of-binary-tree/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| typescript  | 72 ms | 45.4 MB | 2023/08/08 14:14 |

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

function diameterOfBinaryTree(root: TreeNode | null): number {
  let max = 0;
  const recur = (node: TreeNode | null) => {
    if (!node) {
      return 0;
    }

    const left = recur(node.left);
    const right = recur(node.right);

    const rootPathLength = left + right;
    
    const maxPathLength = Math.max(left, right) + 1;

    if (rootPathLength > max) {
      max = rootPathLength;
    }

    return maxPathLength;
  }

  recur(root);

  return max;
};

```
## My Notes - 我的笔记


No notes

