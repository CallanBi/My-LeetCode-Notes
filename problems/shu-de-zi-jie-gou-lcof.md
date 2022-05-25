
# 剑指 Offer 26. 树的子结构  LCOF - 树的子结构

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Tree-树-blue.svg">   <img src="https://img.shields.io/badge/Depth-First Search-深度优先搜索-blue.svg">   <img src="https://img.shields.io/badge/Binary Tree-二叉树-blue.svg">  


## Description - 题目描述

### EN:
English description is not available for the problem. Please switch to Chinese.

### ZH-CN:
<p>输入两棵二叉树A和B，判断B是不是A的子结构。(约定空树不是任意一个树的子结构)</p>

<p>B是A的子结构， 即 A中有出现和B相同的结构和节点值。</p>

<p>例如:<br>
给定的树 A:</p>

<p><code>&nbsp; &nbsp; &nbsp;3<br>
&nbsp; &nbsp; / \<br>
&nbsp; &nbsp;4 &nbsp; 5<br>
&nbsp; / \<br>
&nbsp;1 &nbsp; 2</code><br>
给定的树 B：</p>

<p><code>&nbsp; &nbsp;4&nbsp;<br>
&nbsp; /<br>
&nbsp;1</code><br>
返回 true，因为 B 与 A 的一个子树拥有相同的结构和节点值。</p>

<p><strong>示例 1：</strong></p>

<pre><strong>输入：</strong>A = [1,2,3], B = [3,1]
<strong>输出：</strong>false
</pre>

<p><strong>示例 2：</strong></p>

<pre><strong>输入：</strong>A = [3,4,5,1,2], B = [4,1]
<strong>输出：</strong>true</pre>

<p><strong>限制：</strong></p>

<p><code>0 &lt;= 节点个数 &lt;= 10000</code></p>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/shu-de-zi-jie-gou-lcof/description/)  -  [LeetCode-CN](https://leetcode-cn.com/problems/shu-de-zi-jie-gou-lcof/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| typescript  | 128 ms | 58 MB | 2021/11/05 17:24 |

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

function isSubStructure(A: TreeNode | null, B: TreeNode | null): boolean {
  if (!A || !B) {
    return false;
  }
  return checkIsSameTree(A,B) || isSubStructure(A.left, B) || isSubStructure(A.right, B);
};

const checkIsSameTree: (A: TreeNode | null, B: TreeNode | null) => boolean = (A, B) => {
  if (!B) {
    return true;
  }
  if (!A || A.val !== B.val) {
    return false;
  }
  return checkIsSameTree(A.left, B.left) && checkIsSameTree(A.right, B.right);
}


```
## My Notes - 我的笔记


# 解题思路
第一遍竟然蒙对了。。。神奇。
供参考。

# 代码
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

function isSubStructure(A: TreeNode | null, B: TreeNode | null): boolean {
  if (!A && !B) {
    return true;
  }
  if (!A || !B) {
    return false;
  }

  if (A.val === B.val) {
    return isSubStructure(A.left, B.left) && A.left?.val === B.left?.val && isSubStructure(A.right, B.right) && A.right?.val === B.right?.val || isSubStructure(A.left, B.left) && A.left?.val === B.left?.val && !B.right || isSubStructure(A.right, B.right) && A.right?.val === B.right?.val && !B.left || isSubStructure(A.left, B) || isSubStructure(A.right, B);
  } else {
    return isSubStructure(A.left, B) || isSubStructure(A.right, B);
  }
};
```

# 参考其他人的代码
```typescript
function isSubStructure(A: TreeNode | null, B: TreeNode | null): boolean {
  if (!A || !B) {
    return false;
  }
  return checkIsSameTree(A,B) || isSubStructure(A.left, B) || isSubStructure(A.right, B);
};

const checkIsSameTree: (A: TreeNode | null, B: TreeNode | null) => boolean = (A, B) => {
  if (!B) {
    return true;
  }
  if (!A || A.val !== B.val) {
    return false;
  }
  return checkIsSameTree(A.left, B.left) && checkIsSameTree(A.right, B.right);
}
```

