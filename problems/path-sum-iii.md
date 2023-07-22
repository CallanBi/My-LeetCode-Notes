
# 437. Path Sum III - 路径总和 III

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Tree-树-blue.svg">   <img src="https://img.shields.io/badge/Depth First Search-深度优先搜索-blue.svg">   <img src="https://img.shields.io/badge/Binary Tree-二叉树-blue.svg">  


## Description - 题目描述

### EN:
<p>Given the <code>root</code> of a binary tree and an integer <code>targetSum</code>, return <em>the number of paths where the sum of the values&nbsp;along the path equals</em>&nbsp;<code>targetSum</code>.</p>

<p>The path does not need to start or end at the root or a leaf, but it must go downwards (i.e., traveling only from parent nodes to child nodes).</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2021/04/09/pathsum3-1-tree.jpg" style="width: 450px; height: 386px;" />
<pre>
<strong>Input:</strong> root = [10,5,-3,3,2,null,11,3,-2,null,1], targetSum = 8
<strong>Output:</strong> 3
<strong>Explanation:</strong> The paths that sum to 8 are shown.
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre>
<strong>Input:</strong> root = [5,4,8,11,null,13,4,7,2,null,null,5,1], targetSum = 22
<strong>Output:</strong> 3
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li>The number of nodes in the tree is in the range <code>[0, 1000]</code>.</li>
	<li><code>-10<sup>9</sup> &lt;= Node.val &lt;= 10<sup>9</sup></code></li>
	<li><code>-1000 &lt;= targetSum &lt;= 1000</code></li>
</ul>


### ZH-CN:
<p>给定一个二叉树的根节点 <code>root</code> ，和一个整数 <code>targetSum</code> ，求该二叉树里节点值之和等于 <code>targetSum</code> 的 <strong>路径</strong> 的数目。</p>

<p><strong>路径</strong> 不需要从根节点开始，也不需要在叶子节点结束，但是路径方向必须是向下的（只能从父节点到子节点）。</p>

<p> </p>

<p><strong>示例 1：</strong></p>

<p><img src="https://assets.leetcode.com/uploads/2021/04/09/pathsum3-1-tree.jpg" style="width: 452px; " /></p>

<pre>
<strong>输入：</strong>root = [10,5,-3,3,2,null,11,3,-2,null,1], targetSum = 8
<strong>输出：</strong>3
<strong>解释：</strong>和等于 8 的路径有 3 条，如图所示。
</pre>

<p><strong>示例 2：</strong></p>

<pre>
<strong>输入：</strong>root = [5,4,8,11,null,13,4,7,2,null,null,5,1], targetSum = 22
<strong>输出：</strong>3
</pre>

<p> </p>

<p><strong>提示:</strong></p>

<ul>
	<li>二叉树的节点个数的范围是 <code>[0,1000]</code></li>
	<li><meta charset="UTF-8" /><code>-10<sup>9</sup> <= Node.val <= 10<sup>9</sup></code> </li>
	<li><code>-1000 <= targetSum <= 1000</code> </li>
</ul>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/path-sum-iii/description/)  -  [LeetCode-CN](https://leetcode.cn/problems/path-sum-iii/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| typescript  | 628 ms | 79.7 MB | 2023/07/20 1:03 |

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

function pathSum(root: TreeNode | null, targetSum: number): number {
  let res = 0;

  // for dedup
  const mem: Map<TreeNode, Map<TreeNode, boolean>> = new Map();

  const dfs = (cur: TreeNode | null, parent: TreeNode | null, targetLeft: number) => {
    const path = mem.get(parent)?.get?.(cur);

    const isVisited = path !== undefined;

    if (isVisited) {
      return;
    }

    if (!cur) {
      return;
    }

    if (targetLeft === cur.val) {
      res += 1;
    }

    const paths = mem.get(parent);
    if (paths) {
      paths.set(cur, true);
    } else {
      mem.set(parent, new Map([[cur, true]]));
    }

    dfs(cur.left, parent ?? cur, targetLeft - cur.val);

    dfs(cur.left, null, targetSum);

    dfs(cur.right, parent ?? cur, targetLeft - cur.val);

    dfs(cur.right, null, targetSum);
  }

  dfs(root, null, targetSum);

  return res;
};

```
## My Notes - 我的笔记


 # 自己的思路：剪枝+dfs
 错误的思路：
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

function pathSum(root: TreeNode | null, targetSum: number): number {
  let res = 0;

  const mem: Map<TreeNode, Map<number, number>> = new Map();


  const dfs = (root: TreeNode | null, targetLeft: number, ) => {
    const memNum = mem.get(root)?.get?.(targetLeft);
    if (typeof (memNum) === 'number') {
      res += memNum;
      return;
    }

    if (!root) {
      return;
    }

    if (targetLeft === root.val) {
      res += 1;

      const memRow = mem.get(root);
      if (memRow) {
        const prev = memRow.get(targetLeft);
        memRow.set(targetLeft, prev + 1);
        mem.set(root, memRow);
      } else {
        mem.set(root, new Map([
          [targetLeft, 1]
        ]))
      }
    }

    dfs(root.left, targetLeft - root.val);

    dfs(root.left, targetLeft);

    dfs(root.right, targetLeft - root.val);

    dfs(root.right, targetLeft);
  }

  dfs(root, targetSum);

  return res;
};
 ```
 
 这里错误的原因是，不应该 dfs `targetLeft` ，而是 `target`，因为如果当前路径不存在，则需要重新开始找。
 
 后面想到了正确的思路：dfs遍历树，使用一个二维的Map标记是否访问过这一路径。若访问过，则无论改路径是否合法，都应该剪枝掉。（因为已经访问过知道结果是否合法了）。

这一思路的正确性在于：对于一棵二叉树而言，其父节点到子节点的路径一定是唯一的。

代码：
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

function pathSum(root: TreeNode | null, targetSum: number): number {
  let res = 0;

  // for dedup
  const mem: Map<TreeNode, Map<TreeNode, boolean>> = new Map();

  const dfs = (cur: TreeNode | null, parent: TreeNode | null, targetLeft: number) => {
    const path = mem.get(parent)?.get?.(cur);

    const isVisited = path !== undefined;

    if (isVisited) {
      return;
    }

    if (!cur) {
      return;
    }

    if (targetLeft === cur.val) {
      res += 1;
    }

    const paths = mem.get(parent);
    if (paths) {
      paths.set(cur, true);
    } else {
      mem.set(parent, new Map([[cur, true]]));
    }

    dfs(cur.left, parent ?? cur, targetLeft - cur.val);

    dfs(cur.left, null, targetSum);

    dfs(cur.right, parent ?? cur, targetLeft - cur.val);

    dfs(cur.right, null, targetSum);
  }

  dfs(root, null, targetSum);

  return res;
};

```

