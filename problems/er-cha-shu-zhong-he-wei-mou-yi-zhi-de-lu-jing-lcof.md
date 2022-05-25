
# 剑指 Offer 34. 二叉树中和为某一值的路径 LCOF - 二叉树中和为某一值的路径

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Tree-树-blue.svg">   <img src="https://img.shields.io/badge/Depth-First Search-深度优先搜索-blue.svg">   <img src="https://img.shields.io/badge/Backtracking-回溯-blue.svg">   <img src="https://img.shields.io/badge/Binary Tree-二叉树-blue.svg">  


## Description - 题目描述

### EN:
English description is not available for the problem. Please switch to Chinese.

### ZH-CN:
<p>给你二叉树的根节点 <code>root</code> 和一个整数目标和 <code>targetSum</code> ，找出所有 <strong>从根节点到叶子节点</strong> 路径总和等于给定目标和的路径。</p>

<p><strong>叶子节点</strong> 是指没有子节点的节点。</p>

<p>&nbsp;</p>

<p><strong>示例 1：</strong></p>

<p><img alt="" src="https://assets.leetcode.com/uploads/2021/01/18/pathsumii1.jpg" /></p>

<pre>
<strong>输入：</strong>root = [5,4,8,11,null,13,4,7,2,null,null,5,1], targetSum = 22
<strong>输出：</strong>[[5,4,11,2],[5,8,4,5]]
</pre>

<p><strong>示例 2：</strong></p>

<p><img alt="" src="https://assets.leetcode.com/uploads/2021/01/18/pathsum2.jpg" /></p>

<pre>
<strong>输入：</strong>root = [1,2,3], targetSum = 5
<strong>输出：</strong>[]
</pre>

<p><strong>示例 3：</strong></p>

<pre>
<strong>输入：</strong>root = [1,2], targetSum = 0
<strong>输出：</strong>[]
</pre>

<p>&nbsp;</p>

<p><strong>提示：</strong></p>

<ul>
	<li>树中节点总数在范围 <code>[0, 5000]</code> 内</li>
	<li><code>-1000 &lt;= Node.val &lt;= 1000</code></li>
	<li><code>-1000 &lt;= targetSum &lt;= 1000</code></li>
</ul>

<p>注意：本题与主站 113&nbsp;题相同：<a href="https://leetcode-cn.com/problems/path-sum-ii/">https://leetcode-cn.com/problems/path-sum-ii/</a></p>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/er-cha-shu-zhong-he-wei-mou-yi-zhi-de-lu-jing-lcof/description/)  -  [LeetCode-CN](https://leetcode-cn.com/problems/er-cha-shu-zhong-he-wei-mou-yi-zhi-de-lu-jing-lcof/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| typescript  | 92 ms | 48.5 MB | 2021/11/08 19:29 |

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

function pathSum(root: TreeNode | null, target: number): number[][] {
  if (!root) {
    return [];
  }

  const res: number[][] = [];

  recur(root, [], 0, target, res);

  return res;

};

function recur(root: TreeNode | null, path: number[], sum: number, target: number, res: number[][]): void {
  if (!root) {
    return;
  }

  const newPath = [...path, root.val];
  const newSum = root.val + sum;

  if (newSum === target && !root.left && !root.right) {
    res.push(newPath);
  } else {
    recur(root.left, newPath, newSum, target, res);
    recur(root.right, newPath, newSum, target, res);
  }
}

```
## My Notes - 我的笔记


还是经典递归，记住来过的路径和之前累加的值即可
``` typescript
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

function pathSum(root: TreeNode | null, target: number): number[][] {
  if (!root) {
    return [];
  }

  const res: number[][] = [];

  recur(root, [], 0, target, res);

  return res;

};

function recur(root: TreeNode | null, path: number[], sum: number, target: number, res: number[][]): void {
  if (!root) {
    return;
  }

  const newPath = [...path, root.val];
  const newSum = root.val + sum;

  if (newSum === target && !root.left && !root.right) {
    res.push(newPath);
  } else {
    recur(root.left, newPath, newSum, target, res);
    recur(root.right, newPath, newSum, target, res);
  }
}
```

