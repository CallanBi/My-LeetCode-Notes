
# 剑指 Offer 07. 重建二叉树 LCOF - 重建二叉树

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Tree-树-blue.svg">   <img src="https://img.shields.io/badge/Array-数组-blue.svg">   <img src="https://img.shields.io/badge/Hash Table-哈希表-blue.svg">   <img src="https://img.shields.io/badge/Divide and Conquer-分治-blue.svg">   <img src="https://img.shields.io/badge/Binary Tree-二叉树-blue.svg">  


## Description - 题目描述

### EN:
<p>English description is not available for the problem. Please switch to Chinese.</p>

### ZH-CN:
<p>输入某二叉树的前序遍历和中序遍历的结果，请构建该二叉树并返回其根节点。</p>

<p>假设输入的前序遍历和中序遍历的结果中都不含重复的数字。</p>

<p> </p>

<p><strong>示例 1:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2021/02/19/tree.jpg" />
<pre>
<strong>Input:</strong> preorder = [3,9,20,15,7], inorder = [9,3,15,20,7]
<strong>Output:</strong> [3,9,20,null,null,15,7]
</pre>

<p><strong>示例 2:</strong></p>

<pre>
<strong>Input:</strong> preorder = [-1], inorder = [-1]
<strong>Output:</strong> [-1]
</pre>

<p> </p>

<p><strong>限制：</strong></p>

<p><code>0 <= 节点个数 <= 5000</code></p>

<p> </p>

<p><strong>注意</strong>：本题与主站 105 题重复：<a href="https://leetcode-cn.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/">https://leetcode-cn.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/</a></p>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/zhong-jian-er-cha-shu-lcof/description/)  -  [LeetCode-CN](https://leetcode-cn.com/problems/zhong-jian-er-cha-shu-lcof/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| typescript  | 164 ms | 110.7 MB | 2021/11/02 18:31 |

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

function buildTree(preorder: number[], inorder: number[]): TreeNode | null {
    if ((!preorder[0] && typeof preorder[0] !== 'number')) {
        return null;
    }

    const leftTreeLength = inorder.findIndex(e => e === preorder[0]);
    
    const leftTreePreOrder = preorder.slice(1, 1 + leftTreeLength);
    const leftTreeInOrder = inorder.slice(0, leftTreeLength);

    const rightTreePreOrder = preorder.slice(leftTreeLength + 1);
    const rightTreeInOrder = inorder.slice(leftTreeLength + 1);

    return new TreeNode(preorder[0], buildTree(leftTreePreOrder, leftTreeInOrder), buildTree(rightTreePreOrder, rightTreeInOrder));
};

```
## My Notes - 我的笔记


按照剑指 offer 的思路写的
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

function buildTree(preorder: number[], inorder: number[]): TreeNode | null {
  if (preorder.length === 0 || inorder.length === 0) {
    return null;
  }
  const root = preorder[0];
  const inOrderRootLocation = inorder.findIndex(e => e === root);
  const leftTreeLength = inOrderRootLocation;
  const rightTreeLength = inorder.length - leftTreeLength - 1;

  const leftTreePreOrder = preorder.slice(1, 1 + leftTreeLength);
  const leftTreeInOrder = inorder.slice(0, leftTreeLength);

  const rightTreePreOrder = preorder.slice(1 + leftTreeLength);
  const rightTreeInOrder = inorder.slice(1 + leftTreeLength);

  const leftNode = buildTree(leftTreePreOrder, leftTreeInOrder);
  const rightNode = buildTree(rightTreePreOrder, rightTreeInOrder);

  return new TreeNode(root, leftNode, rightNode);
};
```

按照高赞答案，可以将 InOrder 值作为索引，反向映射地址，然后取 preorder 的 root 值就可以得到 inorder root 所在地址




