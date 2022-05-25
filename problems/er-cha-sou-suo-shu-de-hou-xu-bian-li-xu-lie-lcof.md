
# 剑指 Offer 33. 二叉搜索树的后序遍历序列 LCOF - 二叉搜索树的后序遍历序列

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Stack-栈-blue.svg">   <img src="https://img.shields.io/badge/Tree-树-blue.svg">   <img src="https://img.shields.io/badge/Binary Search Tree-二叉搜索树-blue.svg">   <img src="https://img.shields.io/badge/Recursion-递归-blue.svg">   <img src="https://img.shields.io/badge/Binary Tree-二叉树-blue.svg">   <img src="https://img.shields.io/badge/Monotonic Stack-单调栈-blue.svg">  


## Description - 题目描述

### EN:
English description is not available for the problem. Please switch to Chinese.

### ZH-CN:
<p>输入一个整数数组，判断该数组是不是某二叉搜索树的后序遍历结果。如果是则返回&nbsp;<code>true</code>，否则返回&nbsp;<code>false</code>。假设输入的数组的任意两个数字都互不相同。</p>

<p>&nbsp;</p>

<p>参考以下这颗二叉搜索树：</p>

<pre>     5
    / \
   2   6
  / \
 1   3</pre>

<p><strong>示例 1：</strong></p>

<pre><strong>输入: </strong>[1,6,3,2,5]
<strong>输出: </strong>false</pre>

<p><strong>示例 2：</strong></p>

<pre><strong>输入: </strong>[1,3,2,6,5]
<strong>输出: </strong>true</pre>

<p>&nbsp;</p>

<p><strong>提示：</strong></p>

<ol>
	<li><code>数组长度 &lt;= 1000</code></li>
</ol>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/er-cha-sou-suo-shu-de-hou-xu-bian-li-xu-lie-lcof/description/)  -  [LeetCode-CN](https://leetcode-cn.com/problems/er-cha-sou-suo-shu-de-hou-xu-bian-li-xu-lie-lcof/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| typescript  | 76 ms | 40 MB | 2021/11/08 13:20 |

```typescript

function verifyPostorder(postorder: number[]): boolean {
  if (postorder.length === 0 || postorder.length === 1) {
    return true;
  }

  const root = postorder[postorder.length-1];
  let i = 0;
  for (; i < postorder.length; i++) {
    if (postorder[i] > root) {
      break;
    }
  }

  if (i === postorder.length) {
    return verifyPostorder(postorder.slice(0, postorder.length-1));
  }

  const right = postorder.slice(i, postorder.length-1);
  const left = postorder.slice(0, i);

  if (right.findIndex(e => e < root) !== -1) {
    return false;
  } else {
    return verifyPostorder(left) && verifyPostorder(right);
  }
};

```
## My Notes - 我的笔记


1. 注意递归终止条件（即为 true 时）
2. 当右子树没找到比根结点小的值，则继续递归左右子树，不能不递归或只递归右子树

```typescript
function verifyPostorder(postorder: number[]): boolean {
  if (postorder.length === 0 || postorder.length === 1) {
    return true; // 确定递归终止条件
  }

  const root = postorder[postorder.length-1];
  let i = 0;
  for (; i < postorder.length; i++) {
    if (postorder[i] > root) {
      break;
    }
  }

  if (i === postorder.length) {
    return verifyPostorder(postorder.slice(0, postorder.length-1));
  }

  const right = postorder.slice(i, postorder.length-1);
  const left = postorder.slice(0, i);

  if (right.findIndex(e => e < root) !== -1) {
    return false;
  } else {
    return verifyPostorder(left) && verifyPostorder(right);
  }
};
```


