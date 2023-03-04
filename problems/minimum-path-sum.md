
# 64. Minimum Path Sum - 最小路径和

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Array-数组-blue.svg">   <img src="https://img.shields.io/badge/Dynamic Programming-动态规划-blue.svg">   <img src="https://img.shields.io/badge/Matrix-矩阵-blue.svg">  


## Description - 题目描述

### EN:
<p>Given a <code>m x n</code> <code>grid</code> filled with non-negative numbers, find a path from top left to bottom right, which minimizes the sum of all numbers along its path.</p>

<p><strong>Note:</strong> You can only move either down or right at any point in time.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2020/11/05/minpath.jpg" style="width: 242px; height: 242px;" />
<pre>
<strong>Input:</strong> grid = [[1,3,1],[1,5,1],[4,2,1]]
<strong>Output:</strong> 7
<strong>Explanation:</strong> Because the path 1 &rarr; 3 &rarr; 1 &rarr; 1 &rarr; 1 minimizes the sum.
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre>
<strong>Input:</strong> grid = [[1,2,3],[4,5,6]]
<strong>Output:</strong> 12
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>m == grid.length</code></li>
	<li><code>n == grid[i].length</code></li>
	<li><code>1 &lt;= m, n &lt;= 200</code></li>
	<li><code>0 &lt;= grid[i][j] &lt;= 100</code></li>
</ul>


### ZH-CN:
<p>给定一个包含非负整数的 <code><em>m</em> x <em>n</em></code> 网格 <code>grid</code> ，请找出一条从左上角到右下角的路径，使得路径上的数字总和为最小。</p>

<p><strong>说明：</strong>每次只能向下或者向右移动一步。</p>

<p> </p>

<p><strong>示例 1：</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2020/11/05/minpath.jpg" style="width: 242px; height: 242px;" />
<pre>
<strong>输入：</strong>grid = [[1,3,1],[1,5,1],[4,2,1]]
<strong>输出：</strong>7
<strong>解释：</strong>因为路径 1→3→1→1→1 的总和最小。
</pre>

<p><strong>示例 2：</strong></p>

<pre>
<strong>输入：</strong>grid = [[1,2,3],[4,5,6]]
<strong>输出：</strong>12
</pre>

<p> </p>

<p><strong>提示：</strong></p>

<ul>
	<li><code>m == grid.length</code></li>
	<li><code>n == grid[i].length</code></li>
	<li><code>1 <= m, n <= 200</code></li>
	<li><code>0 <= grid[i][j] <= 100</code></li>
</ul>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/minimum-path-sum/description/)  -  [LeetCode-CN](https://leetcode.cn/problems/minimum-path-sum/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| typescript  | 72 ms | 43.8 MB | 2022/04/14 13:54 |

```typescript

/** 记忆化搜索 */
function minPathSum(grid: number[][]): number {
  const n = grid.length;
  const m = grid[0]?.length;

  // mem 存储访问过的路径最小值
  const mem = new Array(n).fill([]).map(i => new Array(m).fill(-1));

  function dfs(x, y): number {

    if (x === n - 1 && y === m - 1) {
       mem[x][y] = grid[x][y];
       return mem[x][y];
    }

    if (x === n - 1) {
       mem[x][y] = dfs(x, y + 1) + grid[x][y];
       return mem[x][y];
    } 

    if (y === m - 1) {
       mem[x][y] = dfs(x + 1, y) + grid[x][y];
       return mem[x][y];
    } 

    if (mem[x][y] !== -1) {
      return mem[x][y];
    }

    mem[x][y] = Math.min(dfs(x+1, y), dfs(x, y+1)) + grid[x][y];

    return mem[x][y];
  }

  return dfs(0, 0);
};

```
## My Notes - 我的笔记


依然是典型的 dfs 记忆化搜索 / dp 双解法题


