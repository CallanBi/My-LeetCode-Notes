
# 剑指 Offer 47. 礼物的最大价值 LCOF - 礼物的最大价值

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Array-数组-blue.svg">   <img src="https://img.shields.io/badge/Dynamic Programming-动态规划-blue.svg">   <img src="https://img.shields.io/badge/Matrix-矩阵-blue.svg">  


## Description - 题目描述

### EN:
English description is not available for the problem. Please switch to Chinese.

### ZH-CN:
<p>在一个 m*n 的棋盘的每一格都放有一个礼物，每个礼物都有一定的价值（价值大于 0）。你可以从棋盘的左上角开始拿格子里的礼物，并每次向右或者向下移动一格、直到到达棋盘的右下角。给定一个棋盘及其上面的礼物的价值，请计算你最多能拿到多少价值的礼物？</p>

<p>&nbsp;</p>

<p><strong>示例 1:</strong></p>

<pre><strong>输入:</strong> 
<code>[
&nbsp; [1,3,1],
&nbsp; [1,5,1],
&nbsp; [4,2,1]
]</code>
<strong>输出:</strong> <code>12
</code><strong>解释:</strong> 路径 1&rarr;3&rarr;5&rarr;2&rarr;1 可以拿到最多价值的礼物</pre>

<p>&nbsp;</p>

<p>提示：</p>

<ul>
	<li><code>0 &lt; grid.length &lt;= 200</code></li>
	<li><code>0 &lt; grid[0].length &lt;= 200</code></li>
</ul>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/li-wu-de-zui-da-jie-zhi-lcof/description/)  -  [LeetCode-CN](https://leetcode-cn.com/problems/li-wu-de-zui-da-jie-zhi-lcof/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| typescript  | 80 ms | 41 MB | 2021/12/18 19:20 |

```typescript

function maxValue(grid: number[][]): number {
  const m = grid[0].length;
  const n = grid.length;
  if (m === 0 && n === 0) {
    return 0;
  }
  const dp: number[][] = new Array(n).fill([]).map(_ => new Array(m).fill(0));

  for (let i = 0; i < m; i++) {
    dp[0][i] = grid[0].slice(0, i+1).reduce((acc, cur) => acc + cur, 0);
  }

  for (let i = 1; i < n; i++) {
    for (let j = 0; j < m; j++) {
      dp[i][j] = Math.max(dp[i - 1]?.[j] ?? 0, dp[i]?.[j-1] ?? 0) + grid[i][j];
    }
  }

  return dp[n-1][m-1];
};

```
## My Notes - 我的笔记


# 典型的动态规划题
```typescript
function maxValue(grid: number[][]): number {
  const m = grid[0].length;
  const n = grid.length;
  if (m === 0 && n === 0) {
    return 0;
  }
  const dp: number[][] = new Array(n).fill([]).map(_ => new Array(m).fill(0));

  for (let i = 0; i < m; i++) {
    dp[0][i] = grid[0].slice(0, i+1).reduce((acc, cur) => acc + cur, 0);
  }

  for (let i = 1; i < n; i++) {
    for (let j = 0; j < m; j++) {
      dp[i][j] = Math.max(dp[i - 1]?.[j] ?? 0, dp[i]?.[j-1] ?? 0) + grid[i][j];
    }
  }

  return dp[n-1][m-1];
};
```

注意

1. 新建二维数组，记得新建最外层时要 `fill()` 一下。

例如，这样写是不对的：
```typescript
const dp: number[][] = new Array(n).map(_ => new Array(m).fill(0));
```
因为最外没有 `fill()`，所以 `map()` 不起作用。

应该这样：
```typescript
const dp: number[][] = new Array(n).fill([]).map(_ => new Array(m).fill(0));
```

2. 注意循环时看清行和列用哪个。

3. 合理运用 optional chaining 和 `??` 运算符，对数组取不到的 null 和 undefined 进行处理。

