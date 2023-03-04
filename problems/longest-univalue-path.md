
# 687. Longest Univalue Path - 最长同值路径

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Tree-树-blue.svg">   <img src="https://img.shields.io/badge/Depth First Search-深度优先搜索-blue.svg">   <img src="https://img.shields.io/badge/Binary Tree-二叉树-blue.svg">  


## Description - 题目描述

### EN:
<p>Given the <code>root</code> of a binary tree, return <em>the length of the longest path, where each node in the path has the same value</em>. This path may or may not pass through the root.</p>

<p><strong>The length of the path</strong> between two nodes is represented by the number of edges between them.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2020/10/13/ex1.jpg" style="width: 450px; height: 238px;" />
<pre>
<strong>Input:</strong> root = [5,4,5,1,1,null,5]
<strong>Output:</strong> 2
<strong>Explanation:</strong> The shown image shows that the longest path of the same value (i.e. 5).
</pre>

<p><strong class="example">Example 2:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2020/10/13/ex2.jpg" style="width: 450px; height: 238px;" />
<pre>
<strong>Input:</strong> root = [1,4,5,4,4,null,5]
<strong>Output:</strong> 2
<strong>Explanation:</strong> The shown image shows that the longest path of the same value (i.e. 4).
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li>The number of nodes in the tree is in the range <code>[0, 10<sup>4</sup>]</code>.</li>
	<li><code>-1000 &lt;= Node.val &lt;= 1000</code></li>
	<li>The depth of the tree will not exceed <code>1000</code>.</li>
</ul>


### ZH-CN:
<p>给定一个二叉树的<meta charset="UTF-8" />&nbsp;<code>root</code>&nbsp;，返回&nbsp;<em>最长的路径的长度</em> ，这个路径中的&nbsp;<em>每个节点具有相同值</em>&nbsp;。 这条路径可以经过也可以不经过根节点。</p>

<p><strong>两个节点之间的路径长度</strong>&nbsp;由它们之间的边数表示。</p>

<p>&nbsp;</p>

<p><strong>示例 1:</strong></p>

<p><img alt="" src="https://assets.leetcode.com/uploads/2020/10/13/ex1.jpg" /></p>

<pre>
<strong>输入：</strong>root = [5,4,5,1,1,5]
<strong>输出：</strong>2
</pre>

<p><strong>示例 2:</strong></p>

<p><img alt="" src="https://assets.leetcode.com/uploads/2020/10/13/ex2.jpg" /></p>

<pre>
<strong>输入：</strong>root = [1,4,5,4,4,5]
<strong>输出：</strong>2
</pre>

<p>&nbsp;</p>

<p><strong>提示:</strong></p>

<ul>
	<li>树的节点数的范围是<meta charset="UTF-8" />&nbsp;<code>[0, 10<sup>4</sup>]</code>&nbsp;</li>
	<li><code>-1000 &lt;= Node.val &lt;= 1000</code></li>
	<li>树的深度将不超过 <code>1000</code>&nbsp;</li>
</ul>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/longest-univalue-path/description/)  -  [LeetCode-CN](https://leetcode.cn/problems/longest-univalue-path/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| typescript  | 224 ms | 65.7 MB | 2022/09/04 11:31 |

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

function longestUnivaluePath(root: TreeNode | null): number {
  if (!root) {
    return 0;
  }
  let longestPath = -Infinity;
  /** 
  * @returns [withRootPathLength, withoutRootPathLength, rootVal] 
  */
  function findUnivalue(node: TreeNode | null): [number, number, number] {
    if (!node) {
      return [0, 0, -1001];
    }

    const [leftPathWithRootLen, leftPathWithoutRootLen, leftVal] = findUnivalue(node.left);
    const [rightPathWithRootLen, rightPathWithoutRootLen, rightVal] = findUnivalue(node.right);

    if (leftVal === rightVal && leftVal === node.val) {
      longestPath = Math.max(leftPathWithRootLen, rightPathWithRootLen, leftPathWithoutRootLen + rightPathWithoutRootLen + 2, longestPath);
      return [leftPathWithoutRootLen + rightPathWithoutRootLen + 2, Math.max(leftPathWithoutRootLen, rightPathWithoutRootLen) + 1, node.val];
    } else if (leftVal === rightVal && leftVal !== node.val) {
      longestPath = Math.max(leftPathWithoutRootLen, rightPathWithoutRootLen, longestPath);
      return [0, 0, node.val];
    } else if (leftVal !== rightVal && leftVal === node.val) {
      longestPath = Math.max(leftPathWithoutRootLen + 1, longestPath);
      return [leftPathWithoutRootLen + 1, leftPathWithoutRootLen + 1, node.val];
    } else if (leftVal !== rightVal && rightVal === node.val) {
      longestPath = Math.max(rightPathWithoutRootLen + 1, longestPath);
      return [rightPathWithoutRootLen + 1, rightPathWithoutRootLen + 1, node.val];
    } else if (leftVal !== rightVal && leftVal !== node.val && rightVal !== node.val) {
      longestPath = Math.max(longestPath, leftPathWithoutRootLen, rightPathWithoutRootLen);
      return [0, 0, node.val];
    }
  }
  findUnivalue(root);

  return longestPath;
};

```
## My Notes - 我的笔记


一开始我的代码是这样的：
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

function longestUnivaluePath(root: TreeNode | null): number {
  if (!root) {
    return 0;
  }
  let longestPath = -Infinity;
  function findUnivalue(node: TreeNode | null): [number, number] {
    if (!node) {
      return [0, -1001];
    }

    const [leftPathLen, leftVal] = findUnivalue(node.left);
    const [rightPathLen, rightVal] = findUnivalue(node.right);

    if (leftVal === rightVal && leftVal === node.val) {
      longestPath = Math.max(leftPathLen + rightPathLen + 2, longestPath);
      return [leftPathLen + rightPathLen + 2, node.val];
    } else if (leftVal === rightVal && leftVal !== node.val) {
      longestPath = Math.max(leftPathLen, rightPathLen, longestPath);
      return [0, node.val];
    } else if (leftVal !== rightVal && leftVal === node.val) {
      longestPath = Math.max(leftPathLen + 1, longestPath);
      return [leftPathLen + 1, node.val];
    } else if (leftVal !== rightVal && rightVal === node.val) {
      longestPath = Math.max(rightPathLen + 1, longestPath);
      return [rightPathLen + 1, node.val];
    } else if (leftVal !== rightVal && leftVal !== node.val && rightVal !== node.val) {
      longestPath = Math.max(longestPath, leftPathLen, rightPathLen);
      return [0, node.val];
    }
  }
  findUnivalue(root);

  return longestPath;
};
```

直到遇到这个测试用例：```[1,null,1,1,1,1,1,1]``` 我才发现我的算法实际上是整棵树而不是某一路径。

稍加修改一下：
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

function longestUnivaluePath(root: TreeNode | null): number {
  if (!root) {
    return 0;
  }
  let longestPath = -Infinity;
  /** 
  * @returns [withRootPathLength, withoutRootPathLength, rootVal] 
  */
  function findUnivalue(node: TreeNode | null): [number, number, number] {
    if (!node) {
      return [0, 0, -1001];
    }

    const [leftPathWithRootLen, leftPathWithoutRootLen, leftVal] = findUnivalue(node.left);
    const [rightPathWithRootLen, rightPathWithoutRootLen, rightVal] = findUnivalue(node.right);

    if (leftVal === rightVal && leftVal === node.val) {
      longestPath = Math.max(leftPathWithRootLen, rightPathWithRootLen, leftPathWithoutRootLen + rightPathWithoutRootLen + 2, longestPath);
      return [leftPathWithoutRootLen + rightPathWithoutRootLen + 2, Math.max(leftPathWithoutRootLen, rightPathWithoutRootLen) + 1, node.val];
    } else if (leftVal === rightVal && leftVal !== node.val) {
      longestPath = Math.max(leftPathWithoutRootLen, rightPathWithoutRootLen, longestPath);
      return [0, 0, node.val];
    } else if (leftVal !== rightVal && leftVal === node.val) {
      longestPath = Math.max(leftPathWithoutRootLen + 1, longestPath);
      return [leftPathWithoutRootLen + 1, leftPathWithoutRootLen + 1, node.val];
    } else if (leftVal !== rightVal && rightVal === node.val) {
      longestPath = Math.max(rightPathWithoutRootLen + 1, longestPath);
      return [rightPathWithoutRootLen + 1, rightPathWithoutRootLen + 1, node.val];
    } else if (leftVal !== rightVal && leftVal !== node.val && rightVal !== node.val) {
      longestPath = Math.max(longestPath, leftPathWithoutRootLen, rightPathWithoutRootLen);
      return [0, 0, node.val];
    }
  }
  findUnivalue(root);

  return longestPath;
};
```
就OK了。

