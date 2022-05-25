
# 剑指 Offer 27. 二叉树的镜像  LCOF - 二叉树的镜像

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Tree-树-blue.svg">   <img src="https://img.shields.io/badge/Depth First Search-深度优先搜索-blue.svg">   <img src="https://img.shields.io/badge/Breadth First Search-广度优先搜索-blue.svg">   <img src="https://img.shields.io/badge/Binary Tree-二叉树-blue.svg">  


## Description - 题目描述

### EN:
English description is not available for the problem. Please switch to Chinese.

### ZH-CN:
<p>请完成一个函数，输入一个二叉树，该函数输出它的镜像。</p>

<p>例如输入：</p>

<p><code>&nbsp; &nbsp; &nbsp;4<br>
&nbsp; &nbsp;/ &nbsp; \<br>
&nbsp; 2 &nbsp; &nbsp; 7<br>
&nbsp;/ \ &nbsp; / \<br>
1 &nbsp; 3 6 &nbsp; 9</code><br>
镜像输出：</p>

<p><code>&nbsp; &nbsp; &nbsp;4<br>
&nbsp; &nbsp;/ &nbsp; \<br>
&nbsp; 7 &nbsp; &nbsp; 2<br>
&nbsp;/ \ &nbsp; / \<br>
9 &nbsp; 6 3&nbsp; &nbsp;1</code></p>

<p>&nbsp;</p>

<p><strong>示例 1：</strong></p>

<pre><strong>输入：</strong>root = [4,2,7,1,3,6,9]
<strong>输出：</strong>[4,7,2,9,6,3,1]
</pre>

<p>&nbsp;</p>

<p><strong>限制：</strong></p>

<p><code>0 &lt;= 节点个数 &lt;= 1000</code></p>

<p>注意：本题与主站 226 题相同：<a href="https://leetcode-cn.com/problems/invert-binary-tree/">https://leetcode-cn.com/problems/invert-binary-tree/</a></p>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/er-cha-shu-de-jing-xiang-lcof/description/)  -  [LeetCode-CN](https://leetcode.cn/problems/er-cha-shu-de-jing-xiang-lcof/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| typescript  | 80 ms | 39.5 MB | 2021/11/05 17:44 |

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


function mirrorTree(root: TreeNode | null): TreeNode | null {
  switchPosition(root);
  return root;
};

function switchPosition(root: TreeNode | null): void {
  if (!root) {
    return;
  }
  const temp = root.left;
  root.left = root.right;
  root.right = temp;

  switchPosition(root.left);
  switchPosition(root.right);
}

```
## My Notes - 我的笔记


```typescript
// 只需交换左右子树位置即可
function mirrorTree(root: TreeNode | null): TreeNode | null {
  switchPosition(root);
  return root;
};

function switchPosition(root: TreeNode | null): void {
  if (!root) {
    return;
  }
  const temp = root.left;
  root.left = root.right;
  root.right = temp;

  switchPosition(root.left);
  switchPosition(root.right);
}
```

