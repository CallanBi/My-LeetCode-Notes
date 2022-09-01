
# 面试题13. 机器人的运动范围  LCOF - 机器人的运动范围

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Depth First Search-深度优先搜索-blue.svg">   <img src="https://img.shields.io/badge/Breadth First Search-广度优先搜索-blue.svg">   <img src="https://img.shields.io/badge/Dynamic Programming-动态规划-blue.svg">  


## Description - 题目描述

### EN:
English description is not available for the problem. Please switch to Chinese.

### ZH-CN:
<p>地上有一个m行n列的方格，从坐标 <code>[0,0]</code> 到坐标 <code>[m-1,n-1]</code> 。一个机器人从坐标 <code>[0, 0] </code>的格子开始移动，它每次可以向左、右、上、下移动一格（不能移动到方格外），也不能进入行坐标和列坐标的数位之和大于k的格子。例如，当k为18时，机器人能够进入方格 [35, 37] ，因为3+5+3+7=18。但它不能进入方格 [35, 38]，因为3+5+3+8=19。请问该机器人能够到达多少个格子？</p>

<p>&nbsp;</p>

<p><strong>示例 1：</strong></p>

<pre><strong>输入：</strong>m = 2, n = 3, k = 1
<strong>输出：</strong>3
</pre>

<p><strong>示例 2：</strong></p>

<pre><strong>输入：</strong>m = 3, n = 1, k = 0
<strong>输出：</strong>1
</pre>

<p><strong>提示：</strong></p>

<ul>
	<li><code>1 &lt;= n,m &lt;= 100</code></li>
	<li><code>0 &lt;= k&nbsp;&lt;= 20</code></li>
</ul>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/ji-qi-ren-de-yun-dong-fan-wei-lcof/description/)  -  [LeetCode-CN](https://leetcode.cn/problems/ji-qi-ren-de-yun-dong-fan-wei-lcof/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| typescript  | 112 ms | 45.3 MB | 2021/04/09 0:09 |

```typescript

/**
 * 递归模拟机器人移动
 */
const simulateMoving = (matrix: boolean[][], x: number, y: number, k: number, count: { current: number }): void => {
  if (!matrix[x]) {
    return;
  }
  if (!matrix[x][y]) {
    return;
  }

  const rowNum = x.toString().split('').map(r => Number(r));
  const colNum = y.toString().split('').map(r => Number(r));
  const total = rowNum.reduce((acc, cur) => acc + cur, 0) + colNum.reduce((acc, cur) => acc + cur, 0);
  if (total <= k && matrix[x][y]) {
    count.current = count.current + 1;
    matrix[x][y] = false;
    simulateMoving(matrix, x+1, y, k, count);
    simulateMoving(matrix, x-1, y, k, count);
    simulateMoving(matrix, x, y-1, k, count);
    simulateMoving(matrix, x, y+1, k, count);
  } else {
    return;
  }
}

function movingCount(m: number, n: number, k: number): number {
  let count = { current: 0 };

  const matrix = new Array<boolean[]>(m).fill([]).map(i => new Array<boolean>(n).fill(true));

  // 模拟机器人移动
  simulateMoving(matrix, 0, 0, k, count);

  
  return count.current;
};

```
## My Notes - 我的笔记


1. 首先解法不是遍历数组得到所有格子加起来不满足条件，因为机器人只能从(0, 0)开始移动，格子必须是连续的。
2. 要注意被访问过的格子就不能再访问了，否则会无限递归。
```typescript
/**
 * 递归模拟机器人移动
 */
const simulateMoving = (matrix: boolean[][], x: number, y: number, k: number, count: { current: number }): void => {
  if (!matrix[x]) {
    return;
  }
  if (!matrix[x][y]) {
    return;
  }

  const rowNum = x.toString().split('').map(r => Number(r));
  const colNum = y.toString().split('').map(r => Number(r));
  const total = rowNum.reduce((acc, cur) => acc + cur, 0) + colNum.reduce((acc, cur) => acc + cur, 0);
  if (total <= k && matrix[x][y]) {
    count.current = count.current + 1;
    matrix[x][y] = false;
    simulateMoving(matrix, x+1, y, k, count);
    simulateMoving(matrix, x-1, y, k, count);
    simulateMoving(matrix, x, y-1, k, count);
    simulateMoving(matrix, x, y+1, k, count);
  } else {
    return;
  }
}

function movingCount(m: number, n: number, k: number): number {
  let count = { current: 0 };

  const matrix = new Array<boolean[]>(m).fill([]).map(i => new Array<boolean>(n).fill(true));

  // 模拟机器人移动
  simulateMoving(matrix, 0, 0, k, count);

  
  return count.current;
};
```

