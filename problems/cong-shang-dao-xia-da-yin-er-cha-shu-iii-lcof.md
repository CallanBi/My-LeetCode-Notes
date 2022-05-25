
# 剑指 Offer 32 - III. 从上到下打印二叉树 III LCOF - 从上到下打印二叉树 III

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Tree-树-blue.svg">   <img src="https://img.shields.io/badge/Breadth-First Search-广度优先搜索-blue.svg">   <img src="https://img.shields.io/badge/Binary Tree-二叉树-blue.svg">  


## Description - 题目描述

### EN:
English description is not available for the problem. Please switch to Chinese.

### ZH-CN:
<p>请实现一个函数按照之字形顺序打印二叉树，即第一行按照从左到右的顺序打印，第二层按照从右到左的顺序打印，第三行再按照从左到右的顺序打印，其他行以此类推。</p>

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
  [20,9],
  [15,7]
]
</pre>

<p>&nbsp;</p>

<p><strong>提示：</strong></p>

<ol>
	<li><code>节点总数 &lt;= 1000</code></li>
</ol>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/cong-shang-dao-xia-da-yin-er-cha-shu-iii-lcof/description/)  -  [LeetCode-CN](https://leetcode-cn.com/problems/cong-shang-dao-xia-da-yin-er-cha-shu-iii-lcof/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| typescript  | 80 ms | 40.2 MB | 2021/11/08 11:45 |

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
  let isOddLvl = true;

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
      if (!isOddLvl) {
        thisLvlRes = thisLvlRes.reverse(); // 偶数层时，thisLvlRes 反转一下即可
      }
      res.push(thisLvlRes);
      thisLvlRes = [];
      thisLvlCnt = nextLvlCnt; // 当 thisLvlCnt === 0 时才执行这一步，而不是每次循环开头都执行这一步
      nextLvlCnt = 0;
      isOddLvl = !isOddLvl;
    }
  }
  return res;
};

```
## My Notes - 我的笔记


1. 继承剑指 offer 上一题的最朴素想法
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
  let isOddLvl = true;

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
      if (!isOddLvl) {
        thisLvlRes = thisLvlRes.reverse(); // 偶数层时，thisLvlRes 反转一下即可
      }
      res.push(thisLvlRes);
      thisLvlRes = [];
      thisLvlCnt = nextLvlCnt; // 当 thisLvlCnt === 0 时才执行这一步，而不是每次循环开头都执行这一步
      nextLvlCnt = 0;
      isOddLvl = !isOddLvl;
    }
  }
  return res;
};
```

