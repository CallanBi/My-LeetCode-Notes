
# 剑指 Offer 54. 二叉搜索树的第k大节点  LCOF - 二叉搜索树的第k大节点

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Tree-树-blue.svg">   <img src="https://img.shields.io/badge/Depth First Search-深度优先搜索-blue.svg">   <img src="https://img.shields.io/badge/Binary Search Tree-二叉搜索树-blue.svg">   <img src="https://img.shields.io/badge/Binary Tree-二叉树-blue.svg">  


## Description - 题目描述

### EN:
English description is not available for the problem. Please switch to Chinese.

### ZH-CN:
<p>给定一棵二叉搜索树，请找出其中第 <code>k</code> 大的节点的值。</p>

<p>&nbsp;</p>

<p><strong>示例 1:</strong></p>

<pre>
<strong>输入:</strong> root = [3,1,4,null,2], k = 1
   3
  / \
 1   4
  \
&nbsp;  2
<strong>输出:</strong> 4</pre>

<p><strong>示例 2:</strong></p>

<pre>
<strong>输入:</strong> root = [5,3,6,2,4,null,null,1], k = 3
       5
      / \
     3   6
    / \
   2   4
  /
 1
<strong>输出:</strong> 4</pre>

<p>&nbsp;</p>

<p><strong>限制：</strong></p>

<ul>
	<li>1 ≤ k ≤ 二叉搜索树元素个数</li>
</ul>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/er-cha-sou-suo-shu-de-di-kda-jie-dian-lcof/description/)  -  [LeetCode-CN](https://leetcode.cn/problems/er-cha-sou-suo-shu-de-di-kda-jie-dian-lcof/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| typescript  | 72 ms | 50.1 MB | 2022/04/16 18:35 |

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

function kthLargest(root: TreeNode | null, k: number): number {

  const sorted = inOrder(root);

  return sorted[sorted.length - k];

};

function inOrder(root: TreeNode | null): number[] {
  if (!root) {
    return [];
  }

  const left = inOrder(root.left);

  const right = inOrder(root.right);

  return [...left, root.val, ...right];
}

```
## My Notes - 我的笔记


中序遍历二叉搜索树得到的是一个排序的序列。


