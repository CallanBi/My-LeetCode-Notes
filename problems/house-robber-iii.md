
# 337. House Robber III - 打家劫舍 III

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Tree-树-blue.svg">   <img src="https://img.shields.io/badge/Depth First Search-深度优先搜索-blue.svg">   <img src="https://img.shields.io/badge/Dynamic Programming-动态规划-blue.svg">   <img src="https://img.shields.io/badge/Binary Tree-二叉树-blue.svg">  


## Description - 题目描述

### EN:
<p>The thief has found himself a new place for his thievery again. There is only one entrance to this area, called <code>root</code>.</p>

<p>Besides the <code>root</code>, each house has one and only one parent house. After a tour, the smart thief realized that all houses in this place form a binary tree. It will automatically contact the police if <strong>two directly-linked houses were broken into on the same night</strong>.</p>

<p>Given the <code>root</code> of the binary tree, return <em>the maximum amount of money the thief can rob <strong>without alerting the police</strong></em>.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2021/03/10/rob1-tree.jpg" style="width: 277px; height: 293px;" />
<pre>
<strong>Input:</strong> root = [3,2,3,null,3,null,1]
<strong>Output:</strong> 7
<strong>Explanation:</strong> Maximum amount of money the thief can rob = 3 + 3 + 1 = 7.
</pre>

<p><strong class="example">Example 2:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2021/03/10/rob2-tree.jpg" style="width: 357px; height: 293px;" />
<pre>
<strong>Input:</strong> root = [3,4,5,1,3,null,1]
<strong>Output:</strong> 9
<strong>Explanation:</strong> Maximum amount of money the thief can rob = 4 + 5 = 9.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li>The number of nodes in the tree is in the range <code>[1, 10<sup>4</sup>]</code>.</li>
	<li><code>0 &lt;= Node.val &lt;= 10<sup>4</sup></code></li>
</ul>


### ZH-CN:
<p>小偷又发现了一个新的可行窃的地区。这个地区只有一个入口，我们称之为<meta charset="UTF-8" />&nbsp;<code>root</code>&nbsp;。</p>

<p>除了<meta charset="UTF-8" />&nbsp;<code>root</code>&nbsp;之外，每栋房子有且只有一个“父“房子与之相连。一番侦察之后，聪明的小偷意识到“这个地方的所有房屋的排列类似于一棵二叉树”。 如果 <strong>两个直接相连的房子在同一天晚上被打劫</strong> ，房屋将自动报警。</p>

<p>给定二叉树的&nbsp;<code>root</code>&nbsp;。返回&nbsp;<em><strong>在不触动警报的情况下</strong>&nbsp;，小偷能够盗取的最高金额</em>&nbsp;。</p>

<p>&nbsp;</p>

<p><strong>示例 1:</strong></p>

<p><img alt="" src="https://assets.leetcode.com/uploads/2021/03/10/rob1-tree.jpg" /></p>

<pre>
<strong>输入: </strong>root = [3,2,3,null,3,null,1]
<strong>输出:</strong> 7 
<strong>解释:</strong>&nbsp;小偷一晚能够盗取的最高金额 3 + 3 + 1 = 7</pre>

<p><strong>示例 2:</strong></p>

<p><img alt="" src="https://assets.leetcode.com/uploads/2021/03/10/rob2-tree.jpg" /></p>

<pre>
<strong>输入: </strong>root = [3,4,5,1,3,null,1]
<strong>输出:</strong> 9
<strong>解释:</strong>&nbsp;小偷一晚能够盗取的最高金额 4 + 5 = 9
</pre>

<p>&nbsp;</p>

<p><strong>提示：</strong></p>

<p><meta charset="UTF-8" /></p>

<ul>
	<li>树的节点数在&nbsp;<code>[1, 10<sup>4</sup>]</code> 范围内</li>
	<li><code>0 &lt;= Node.val &lt;= 10<sup>4</sup></code></li>
</ul>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/house-robber-iii/description/)  -  [LeetCode-CN](https://leetcode.cn/problems/house-robber-iii/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| typescript  | 76 ms | 47.3 MB | 2023/04/09 14:58 |

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

function rob(root: TreeNode | null): number {
  const dp: Map<TreeNode, number[]> = new Map();

  const postOrder = (node: TreeNode) => {
    if (!node) {
      return;
    }

    postOrder(node.left);
    postOrder(node.right);

    const left0 = dp.get(node.left)?.[0] || 0;
    const right0 = dp.get(node.right)?.[0] || 0;
    const left1 = dp.get(node.left)?.[1] || 0;
    const right1 = dp.get(node.right)?.[1] || 0;

    const zero = Math.max(left0 + right0, left0 + right1, left1 + right0, left1 + right1);

    const one = node.val + left0 + right0;

    dp.set(node, [
      zero, one
    ]);
  }

  postOrder(root);

  return Math.max(dp.get(root)?.[0] || 0, dp.get(root)?.[1] || 0);

};

```
## My Notes - 我的笔记


# 树形dp
`dp[n][0]` 表示不偷 `n` 节点时的最大金额，`dp[n][1]` 表示偷 `n `节点时的最大金额。
思路： 后序遍历🎄，状态转移如下：
$dp[n][0] = max\{dp[n.left][0] + dp[m.right][0], dp[n.left][0] + dp[n][right][1], dp[n.left][1]+dp[n.right][0], dp[n.left][1] + dp[n.right][1]\}$

$dp[n][1] = n.val + dp[n.left][0] + dp[n.right][0]$

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

function rob(root: TreeNode | null): number {
  const dp: Map<TreeNode, number[]> = new Map();

  const postOrder = (node: TreeNode) => {
    if (!node) {
      return;
    }

    postOrder(node.left);
    postOrder(node.right);

    const left0 = dp.get(node.left)?.[0] || 0;
    const right0 = dp.get(node.right)?.[0] || 0;
    const left1 = dp.get(node.left)?.[1] || 0;
    const right1 = dp.get(node.right)?.[1] || 0;

    const zero = Math.max(left0 + right0, left0 + right1, left1 + right0, left1 + right1);

    const one = node.val + left0 + right0;

    dp.set(node, [
      zero, one
    ]);
  }

  postOrder(root);

  return Math.max(dp.get(root)?.[0] || 0, dp.get(root)?.[1] || 0);

};
```

后来发现`dp[n][0]` 可以简化成：

$dp[n][0] = max\{dp[n.left][0], dp[n.left][1]\} + max\{dp[n.right][0], dp[n.right][1]\}$


