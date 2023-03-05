
# 200. Number of Islands - 岛屿数量

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Depth First Search-深度优先搜索-blue.svg">   <img src="https://img.shields.io/badge/Breadth First Search-广度优先搜索-blue.svg">   <img src="https://img.shields.io/badge/Union Find-并查集-blue.svg">   <img src="https://img.shields.io/badge/Array-数组-blue.svg">   <img src="https://img.shields.io/badge/Matrix-矩阵-blue.svg">  


## Description - 题目描述

### EN:
<p>Given an <code>m x n</code> 2D binary grid <code>grid</code> which represents a map of <code>&#39;1&#39;</code>s (land) and <code>&#39;0&#39;</code>s (water), return <em>the number of islands</em>.</p>

<p>An <strong>island</strong> is surrounded by water and is formed by connecting adjacent lands horizontally or vertically. You may assume all four edges of the grid are all surrounded by water.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input:</strong> grid = [
  [&quot;1&quot;,&quot;1&quot;,&quot;1&quot;,&quot;1&quot;,&quot;0&quot;],
  [&quot;1&quot;,&quot;1&quot;,&quot;0&quot;,&quot;1&quot;,&quot;0&quot;],
  [&quot;1&quot;,&quot;1&quot;,&quot;0&quot;,&quot;0&quot;,&quot;0&quot;],
  [&quot;0&quot;,&quot;0&quot;,&quot;0&quot;,&quot;0&quot;,&quot;0&quot;]
]
<strong>Output:</strong> 1
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre>
<strong>Input:</strong> grid = [
  [&quot;1&quot;,&quot;1&quot;,&quot;0&quot;,&quot;0&quot;,&quot;0&quot;],
  [&quot;1&quot;,&quot;1&quot;,&quot;0&quot;,&quot;0&quot;,&quot;0&quot;],
  [&quot;0&quot;,&quot;0&quot;,&quot;1&quot;,&quot;0&quot;,&quot;0&quot;],
  [&quot;0&quot;,&quot;0&quot;,&quot;0&quot;,&quot;1&quot;,&quot;1&quot;]
]
<strong>Output:</strong> 3
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>m == grid.length</code></li>
	<li><code>n == grid[i].length</code></li>
	<li><code>1 &lt;= m, n &lt;= 300</code></li>
	<li><code>grid[i][j]</code> is <code>&#39;0&#39;</code> or <code>&#39;1&#39;</code>.</li>
</ul>


### ZH-CN:
<p>给你一个由 <code>'1'</code>（陆地）和 <code>'0'</code>（水）组成的的二维网格，请你计算网格中岛屿的数量。</p>

<p>岛屿总是被水包围，并且每座岛屿只能由水平方向和/或竖直方向上相邻的陆地连接形成。</p>

<p>此外，你可以假设该网格的四条边均被水包围。</p>

<p> </p>

<p><strong>示例 1：</strong></p>

<pre>
<strong>输入：</strong>grid = [
  ["1","1","1","1","0"],
  ["1","1","0","1","0"],
  ["1","1","0","0","0"],
  ["0","0","0","0","0"]
]
<strong>输出：</strong>1
</pre>

<p><strong>示例 2：</strong></p>

<pre>
<strong>输入：</strong>grid = [
  ["1","1","0","0","0"],
  ["1","1","0","0","0"],
  ["0","0","1","0","0"],
  ["0","0","0","1","1"]
]
<strong>输出：</strong>3
</pre>

<p> </p>

<p><strong>提示：</strong></p>

<ul>
	<li><code>m == grid.length</code></li>
	<li><code>n == grid[i].length</code></li>
	<li><code>1 <= m, n <= 300</code></li>
	<li><code>grid[i][j]</code> 的值为 <code>'0'</code> 或 <code>'1'</code></li>
</ul>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/number-of-islands/description/)  -  [LeetCode-CN](https://leetcode.cn/problems/number-of-islands/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| typescript  | 88 ms | 44.9 MB | 2023/03/05 18:00 |

```typescript

function numIslands(grid: string[][]): number {
  let res = 0;

  const n = grid[0].length, m = grid.length;

  const mem: boolean[][] = new Array<boolean[][]>(m).fill([]).map(i => new Array(n).fill(false));

  const labelVisited = (i: number, j: number) => {
     if (i === m || j === n || i < 0 || j < 0) {
      return;
    }

    if (mem[i][j] === true) {
      return;
    }

    if (grid[i][j] === '1') {
      mem[i][j] = true;
    } else {
      return;
    }

    labelVisited(i + 1, j);
    labelVisited(i, j + 1);
    labelVisited(i, j - 1);
    labelVisited(i - 1, j);
  }

  for (let i = 0; i < m; i++) {
    for (let j = 0; j < n; j++) {
      if (grid[i][j] === "1" && mem[i][j] === false) {
        labelVisited(i, j);
        res += 1;
      }
    }
  }

  return res;
};

```
## My Notes - 我的笔记


记忆化搜索+dfs 即可。
```typescript
function numIslands(grid: string[][]): number {
  let res = 0;

  const n = grid[0].length, m = grid.length;

  const mem: boolean[][] = new Array<boolean[][]>(m).fill([]).map(i => new Array(n).fill(false));

  const labelVisited = (i: number, j: number) => {
     if (i === m || j === n || i < 0 || j < 0) {
      return;
    }

    if (mem[i][j] === true) {
      return;
    }

    if (grid[i][j] === '1') {
      mem[i][j] = true;
    } else {
      return;
    }

    labelVisited(i + 1, j);
    labelVisited(i, j + 1);
    labelVisited(i, j - 1);
    labelVisited(i - 1, j);
  }

  for (let i = 0; i < m; i++) {
    for (let j = 0; j < n; j++) {
      if (grid[i][j] === "1" && mem[i][j] === false) {
        labelVisited(i, j);
        res += 1;
      }
    }
  }

  return res;
};
```

