
# 剑指 Offer 32 - I. 从上到下打印二叉树 LCOF - 从上到下打印二叉树

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Tree-树-blue.svg">   <img src="https://img.shields.io/badge/Breadth First Search-广度优先搜索-blue.svg">   <img src="https://img.shields.io/badge/Binary Tree-二叉树-blue.svg">  


## Description - 题目描述

### EN:
English description is not available for the problem. Please switch to Chinese.

### ZH-CN:
<p>从上到下打印出二叉树的每个节点，同一层的节点按照从左到右的顺序打印。</p>

<p>&nbsp;</p>

<p>例如:<br>
给定二叉树:&nbsp;<code>[3,9,20,null,null,15,7]</code>,</p>

<pre>    3
   / \
  9  20
    /  \
   15   7
</pre>

<p>返回：</p>

<pre>[3,9,20,15,7]
</pre>

<p>&nbsp;</p>

<p><strong>提示：</strong></p>

<ol>
	<li><code>节点总数 &lt;= 1000</code></li>
</ol>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/cong-shang-dao-xia-da-yin-er-cha-shu-lcof/description/)  -  [LeetCode-CN](https://leetcode.cn/problems/cong-shang-dao-xia-da-yin-er-cha-shu-lcof/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| typescript  | 80 ms | 40.2 MB | 2021/11/07 21:19 |

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

/**
 * 二叉树的层序遍历，利用队列
 */
function levelOrder(root: TreeNode | null): number[] {
  if (!root) {
    return [];
  }
  const queue: TreeNode[]  = [];
  const res: number[] = [];

  queue.push(root);

  while(queue.length > 0) {
    const node = queue.shift();
    if (node) {
      res.push(node.val);
    }
    if (node.left) {
      queue.push(node.left);
    }
    if (node.right) {
      queue.push(node.right);
    }
  }

  return res;
};

```
## My Notes - 我的笔记


基本算法，没什么好说的
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

/**
 * 二叉树的层序遍历（广度优先遍历），利用队列
 */
function levelOrder(root: TreeNode | null): number[] {
  if (!root) {
    return [];
  }
  const queue: TreeNode[]  = [];
  const res: number[] = [];

  queue.push(root);

  while(queue.length > 0) {
    const node = queue.shift();
    if (node) {
      res.push(node.val);
    }
    if (node.left) {
      queue.push(node.left);
    }
    if (node.right) {
      queue.push(node.right);
    }
  }

  return res;
};
```
广度优先遍历有向图，也可以用队列实现：

首先把起始节点放入队列，接下来每次从队列头部取出一个节点，遍历这个节点之后把它能到达的节点都加入队列。

重复该过程，直到队列中节点为空。

