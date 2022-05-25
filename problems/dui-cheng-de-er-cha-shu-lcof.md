
# 剑指 Offer 28. 对称的二叉树  LCOF - 对称的二叉树

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Tree-树-blue.svg">   <img src="https://img.shields.io/badge/Depth-First Search-深度优先搜索-blue.svg">   <img src="https://img.shields.io/badge/Breadth-First Search-广度优先搜索-blue.svg">   <img src="https://img.shields.io/badge/Binary Tree-二叉树-blue.svg">  


## Description - 题目描述

### EN:
English description is not available for the problem. Please switch to Chinese.

### ZH-CN:
<p>请实现一个函数，用来判断一棵二叉树是不是对称的。如果一棵二叉树和它的镜像一样，那么它是对称的。</p>

<p>例如，二叉树&nbsp;[1,2,2,3,4,4,3] 是对称的。</p>

<p><code>&nbsp; &nbsp; 1<br>
&nbsp; &nbsp;/ \<br>
&nbsp; 2 &nbsp; 2<br>
&nbsp;/ \ / \<br>
3 &nbsp;4 4 &nbsp;3</code><br>
但是下面这个&nbsp;[1,2,2,null,3,null,3] 则不是镜像对称的:</p>

<p><code>&nbsp; &nbsp; 1<br>
&nbsp; &nbsp;/ \<br>
&nbsp; 2 &nbsp; 2<br>
&nbsp; &nbsp;\ &nbsp; \<br>
&nbsp; &nbsp;3 &nbsp; &nbsp;3</code></p>

<p>&nbsp;</p>

<p><strong>示例 1：</strong></p>

<pre><strong>输入：</strong>root = [1,2,2,3,4,4,3]
<strong>输出：</strong>true
</pre>

<p><strong>示例 2：</strong></p>

<pre><strong>输入：</strong>root = [1,2,2,null,3,null,3]
<strong>输出：</strong>false</pre>

<p>&nbsp;</p>

<p><strong>限制：</strong></p>

<p><code>0 &lt;= 节点个数 &lt;= 1000</code></p>

<p>注意：本题与主站 101 题相同：<a href="https://leetcode-cn.com/problems/symmetric-tree/">https://leetcode-cn.com/problems/symmetric-tree/</a></p>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/dui-cheng-de-er-cha-shu-lcof/description/)  -  [LeetCode-CN](https://leetcode-cn.com/problems/dui-cheng-de-er-cha-shu-lcof/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| typescript  | 88 ms | 40.2 MB | 2021/11/06 20:29 |

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

function isSymmetric(root: TreeNode | null): boolean {
  if (!root) {
    return true;
  }

  const converted = new TreeNode();

  convertTree(root, converted);

  return recur(root, converted);
};

function recur(origin: TreeNode | null, converted: TreeNode | null): boolean {
  if (!origin && !converted) {
    return true;
  }
  if (!origin || !converted) {
    return false;
  }
  return origin.val === converted.val && recur(origin.left, converted.left) && recur(origin.right, converted.right);
}

function convertTree(root: TreeNode | null, copyied: TreeNode | null): void {
  if (!root && !copyied) {
    return;
  }

  if (!copyied) {
    copyied = new TreeNode(root.val);
  }

  if (!root) {
    copyied = null;
    return;
  }

  copyied.val = root.val;
  copyied.left = root.right? new TreeNode() : null;
  copyied.right = root.left? new TreeNode() : null;

  convertTree(root.left, copyied.right);
  convertTree(root.right, copyied.left);
}

```
## My Notes - 我的笔记


解法一：递归遍历
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

function isSymmetric(root: TreeNode | null): boolean {
  if (!root) {
    return true;
  }
  return recur(root, root);
};

function recur(left: TreeNode | null, right: TreeNode | null): boolean {
  if (!left && !right) {
    return true;
  }

  if (!left || !right) {
    return false;
  }

  return (left.val === right.val) && recur(left.left, right.right) && recur(left.right, right.left);
}
```

解法二：先交换左右节点，再遍历两棵树看看是否一样
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

function isSymmetric(root: TreeNode | null): boolean {
  if (!root) {
    return true;
  }

  const converted = new TreeNode();

  convertTree(root, converted);

  return recur(root, converted);
};

function recur(origin: TreeNode | null, converted: TreeNode | null): boolean {
  if (!origin && !converted) {
    return true;
  }
  if (!origin || !converted) {
    return false;
  }
  return origin.val === converted.val && recur(origin.left, converted.left) && recur(origin.right, converted.right);
}

function convertTree(root: TreeNode | null, copyied: TreeNode | null): void {
  if (!root && !copyied) {
    return;
  }

  if (!copyied) {
    copyied = new TreeNode(root.val);
  }

  if (!root) {
    copyied = null;
    return;
  }

  copyied.val = root.val;
  copyied.left = root.right? new TreeNode() : null;
  copyied.right = root.left? new TreeNode() : null;

  convertTree(root.left, copyied.right);
  convertTree(root.right, copyied.left);
}
```

