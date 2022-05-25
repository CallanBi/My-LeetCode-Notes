
# 剑指 Offer 55 - I. 二叉树的深度 LCOF - 二叉树的深度

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Tree-树-blue.svg">   <img src="https://img.shields.io/badge/Depth First Search-深度优先搜索-blue.svg">   <img src="https://img.shields.io/badge/Breadth First Search-广度优先搜索-blue.svg">   <img src="https://img.shields.io/badge/Binary Tree-二叉树-blue.svg">  


## Description - 题目描述

### EN:
<p>English description is not available for the problem. Please switch to Chinese.</p>


### ZH-CN:
<p>输入一棵二叉树的根节点，求该树的深度。从根节点到叶节点依次经过的节点（含根、叶节点）形成树的一条路径，最长路径的长度为树的深度。</p>

<p>例如：</p>

<p>给定二叉树 <code>[3,9,20,null,null,15,7]</code>，</p>

<pre>    3
   / \
  9  20
    /  \
   15   7</pre>

<p>返回它的最大深度&nbsp;3 。</p>

<p>&nbsp;</p>

<p><strong>提示：</strong></p>

<ol>
	<li><code>节点总数 &lt;= 10000</code></li>
</ol>

<p>注意：本题与主站 104&nbsp;题相同：<a href="https://leetcode-cn.com/problems/maximum-depth-of-binary-tree/">https://leetcode-cn.com/problems/maximum-depth-of-binary-tree/</a></p>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/er-cha-shu-de-shen-du-lcof/description/)  -  [LeetCode-CN](https://leetcode.cn/problems/er-cha-shu-de-shen-du-lcof/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| typescript  | 68 ms | 46.1 MB | 2022/04/16 18:55 |

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

const mem = new Map<TreeNode | null, number>();

function maxDepth(root: TreeNode | null): number {
  return recur(root);
};

function recur(node: TreeNode | null): number {
  if (!node) {
    return 0;
  }

  if (mem.has(node)) {
    return mem.get(node);
  }

  const leftDepth = recur(node.left);
  const rigthDepth = recur(node.right);

  const res = Math.max(leftDepth, rigthDepth) + 1;

  mem.set(node, res)

  return res;

}

```
## My Notes - 我的笔记


dfs 遍历二叉树，使用记忆化搜索优化性能。

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

const mem = new Map<TreeNode | null, number>();

function maxDepth(root: TreeNode | null): number {
  return recur(root);
};

function recur(node: TreeNode | null): number {
  if (!node) {
    return 0;
  }

  if (mem.has(node)) {
    return mem.get(node);
  }

  const leftDepth = recur(node.left);
  const rigthDepth = recur(node.right);
  
  const res = Math.max(leftDepth, rigthDepth) + 1;

  mem.set(node, res)

  return res;

}
```


