
# 剑指 Offer 55 - II. 平衡二叉树 LCOF - 平衡二叉树

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Tree-树-blue.svg">   <img src="https://img.shields.io/badge/Depth First Search-深度优先搜索-blue.svg">   <img src="https://img.shields.io/badge/Binary Tree-二叉树-blue.svg">  


## Description - 题目描述

### EN:
<p>English description is not available for the problem. Please switch to Chinese.</p>

### ZH-CN:
<p>输入一棵二叉树的根节点，判断该树是不是平衡二叉树。如果某二叉树中任意节点的左右子树的深度相差不超过1，那么它就是一棵平衡二叉树。</p>

<p> </p>

<p><strong>示例 1:</strong></p>

<p>给定二叉树 <code>[3,9,20,null,null,15,7]</code></p>

<pre>
    3
   / \
  9  20
    /  \
   15   7</pre>

<p>返回 <code>true</code> 。<br />
<br />
<strong>示例 2:</strong></p>

<p>给定二叉树 <code>[1,2,2,3,3,null,null,4,4]</code></p>

<pre>
       1
      / \
     2   2
    / \
   3   3
  / \
 4   4
</pre>

<p>返回 <code>false</code> 。</p>

<p> </p>

<p><strong>限制：</strong></p>

<ul>
	<li><code>0 <= 树的结点个数 <= 10000</code></li>
</ul>

<p>注意：本题与主站 110 题相同：<a href="https://leetcode-cn.com/problems/balanced-binary-tree/">https://leetcode-cn.com/problems/balanced-binary-tree/</a></p>

<p> </p>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/ping-heng-er-cha-shu-lcof/description/)  -  [LeetCode-CN](https://leetcode.cn/problems/ping-heng-er-cha-shu-lcof/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| typescript  | 68 ms | 49.1 MB | 2022/04/17 17:00 |

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

function isBalanced(root: TreeNode | null): boolean {

  let isBalancedTree = true;

  function recur(node: TreeNode | null): number {
    if (!node) {
      return 0;
    }

    if (mem.has(node)) {
      return mem.get(node);
    }

    const leftDepth = recur(node.left);
    const rigthDepth = recur(node.right);

    if (Math.abs(leftDepth - rigthDepth) > 1) {
      isBalancedTree = false;
    }

    const res = Math.max(leftDepth, rigthDepth) + 1;

    mem.set(node, res)

    return res;

  }

  recur(root);

  return isBalancedTree;

};

```
## My Notes - 我的笔记


与求二叉树的深度一致，用一个外部变量保存是否是平衡树。

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

function isBalanced(root: TreeNode | null): boolean {

  let isBalancedTree = true;

  function recur(node: TreeNode | null): number {
    if (!node) {
      return 0;
    }

    if (mem.has(node)) {
      return mem.get(node);
    }

    const leftDepth = recur(node.left);
    const rigthDepth = recur(node.right);

    if (Math.abs(leftDepth - rigthDepth) > 1) {
      isBalancedTree = false;
    }

    const res = Math.max(leftDepth, rigthDepth) + 1;

    mem.set(node, res)

    return res;

  }

  recur(root);

  return isBalancedTree;

};
```


