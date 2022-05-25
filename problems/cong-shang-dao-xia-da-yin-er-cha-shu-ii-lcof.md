
# 剑指 Offer 32 - II. 从上到下打印二叉树 II LCOF - 从上到下打印二叉树 II

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Tree-树-blue.svg">   <img src="https://img.shields.io/badge/Breadth First Search-广度优先搜索-blue.svg">   <img src="https://img.shields.io/badge/Binary Tree-二叉树-blue.svg">  


## Description - 题目描述

### EN:
English description is not available for the problem. Please switch to Chinese.

### ZH-CN:
<p>从上到下按层打印二叉树，同一层的节点按从左到右的顺序打印，每一层打印到一行。</p>

<p>&nbsp;</p>

<p>例如:<br>
给定二叉树:&nbsp;<code>[3,9,20,null,null,15,7]</code>,</p>

<pre>    3
   / \
  9  20
    /  \
   15   7
</pre>

<p>返回其层次遍历结果：</p>

<pre>[
  [3],
  [9,20],
  [15,7]
]
</pre>

<p>&nbsp;</p>

<p><strong>提示：</strong></p>

<ol>
	<li><code>节点总数 &lt;= 1000</code></li>
</ol>

<p>注意：本题与主站 102 题相同：<a href="https://leetcode-cn.com/problems/binary-tree-level-order-traversal/">https://leetcode-cn.com/problems/binary-tree-level-order-traversal/</a></p>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/cong-shang-dao-xia-da-yin-er-cha-shu-ii-lcof/description/)  -  [LeetCode-CN](https://leetcode.cn/problems/cong-shang-dao-xia-da-yin-er-cha-shu-ii-lcof/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| typescript  | 84 ms | 39.7 MB | 2021/11/08 10:57 |

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

function levelOrder(root: TreeNode | null): number[][] {
  if (!root) {
    return [];
  }

  const res: number[][] = [];
  const assitantStack: TreeNode[] = [];

  assitantStack.push(root);
  let thisLvlCnt = 1, nextLvlCnt = 0;

  let thisLvlRes: number[] = [];

  while(assitantStack.length > 0) {
    const node = assitantStack.shift();
    if (node) {
      thisLvlRes.push(node.val);
      thisLvlCnt--;
    }
    if (node.left) {
      assitantStack.push(node.left);
      nextLvlCnt++;
    }
    if (node.right) {
      assitantStack.push(node.right);
      nextLvlCnt++;
    }
    if (thisLvlCnt === 0) {
      res.push(thisLvlRes);
      thisLvlRes = [];
      thisLvlCnt = nextLvlCnt;
      nextLvlCnt = 0;
    }
  }
  return res;
};

```
## My Notes - 我的笔记


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

function levelOrder(root: TreeNode | null): number[][] {
  if (!root) {
    return [];
  }

  const res: number[][] = [];
  const assitantStack: TreeNode[] = [];

  assitantStack.push(root);
  let thisLvlCnt = 1, nextLvlCnt = 0;

  let thisLvlRes: number[] = [];

  while(assitantStack.length > 0) {
    const node = assitantStack.shift();
    if (node) {
      thisLvlRes.push(node.val);
      thisLvlCnt--;
    }
    if (node.left) {
      assitantStack.push(node.left);
      nextLvlCnt++;
    }
    if (node.right) {
      assitantStack.push(node.right);
      nextLvlCnt++;
    }
    if (thisLvlCnt === 0) {
      res.push(thisLvlRes);
      thisLvlRes = [];
      thisLvlCnt = nextLvlCnt; // 当 thisLvlCnt === 0 时才执行这一步，而不是每次循环开头都执行这一步
      nextLvlCnt = 0;
    }
  }
  return res;
};
```

