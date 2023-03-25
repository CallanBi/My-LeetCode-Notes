
# 279. Perfect Squares - 完全平方数

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Breadth First Search-广度优先搜索-blue.svg">   <img src="https://img.shields.io/badge/Math-数学-blue.svg">   <img src="https://img.shields.io/badge/Dynamic Programming-动态规划-blue.svg">  


## Description - 题目描述

### EN:
<p>Given an integer <code>n</code>, return <em>the least number of perfect square numbers that sum to</em> <code>n</code>.</p>

<p>A <strong>perfect square</strong> is an integer that is the square of an integer; in other words, it is the product of some integer with itself. For example, <code>1</code>, <code>4</code>, <code>9</code>, and <code>16</code> are perfect squares while <code>3</code> and <code>11</code> are not.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input:</strong> n = 12
<strong>Output:</strong> 3
<strong>Explanation:</strong> 12 = 4 + 4 + 4.
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre>
<strong>Input:</strong> n = 13
<strong>Output:</strong> 2
<strong>Explanation:</strong> 13 = 4 + 9.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= n &lt;= 10<sup>4</sup></code></li>
</ul>


### ZH-CN:
<p>给你一个整数 <code>n</code> ，返回 <em>和为 <code>n</code> 的完全平方数的最少数量</em> 。</p>

<p><strong>完全平方数</strong> 是一个整数，其值等于另一个整数的平方；换句话说，其值等于一个整数自乘的积。例如，<code>1</code>、<code>4</code>、<code>9</code> 和 <code>16</code> 都是完全平方数，而 <code>3</code> 和 <code>11</code> 不是。</p>

<p>&nbsp;</p>

<p><strong>示例&nbsp;1：</strong></p>

<pre>
<strong>输入：</strong>n = <code>12</code>
<strong>输出：</strong>3 
<strong>解释：</strong><code>12 = 4 + 4 + 4</code></pre>

<p><strong>示例 2：</strong></p>

<pre>
<strong>输入：</strong>n = <code>13</code>
<strong>输出：</strong>2
<strong>解释：</strong><code>13 = 4 + 9</code></pre>
&nbsp;

<p><strong>提示：</strong></p>

<ul>
	<li><code>1 &lt;= n &lt;= 10<sup>4</sup></code></li>
</ul>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/perfect-squares/description/)  -  [LeetCode-CN](https://leetcode.cn/problems/perfect-squares/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| typescript  | 116 ms | 47.7 MB | 2023/03/25 21:14 |

```typescript

function numSquares(n: number): number {
  if (n === 1) {
    return 1;
  }

  const dp: number[] = [];

  dp[0] = 0;
  dp[1] = 1;

  for (let i = 2; i <= n; i++) {
    let min = +Infinity;
    for (let j = 1; j <= Math.sqrt(i); j++) {
      let ans = 1 + dp[i - j * j];
      min = Math.min(ans, min);
    }
    dp[i] = min;
  }
  return dp[n];
};

```
## My Notes - 我的笔记


# 动态规划
考虑用动态规划解。
状态转移方程：$min \{ dp[i]+dp[n-i] \}, i \in [\sqrt n, n]$
最开始的代码，会超出时间限制：
```typescript
function numSquares(n: number): number {
  if (n === 1) {
    return 1;
  }

  const dp: number[] = [];

  dp[0] = 0;
  dp[1] = 1;

  for (let i = 2; i <= n; i++) {
    let min = +Infinity;
    for (let j = Math.floor(Math.sqrt(i)); j <= n; j++) {
      let ans = 0;
      if (j === Math.sqrt(i)) {
        ans = 1;
      } else {
        ans = dp[j] + dp[i - j];
      }
      if (ans < min) {
        min = ans;
      }
    }
    dp[i] = min;
  }

  return dp[n];
};
```

后来看了题解，实际上换一个状态转移方程即可:
$min \{ 1 +dp[n - i^2] \}, i \in [1, \sqrt n]$

```typescript
function numSquares(n: number): number {
  if (n === 1) {
    return 1;
  }

  const dp: number[] = [];

  dp[0] = 0;
  dp[1] = 1;

  for (let i = 2; i <= n; i++) {
    let min = +Infinity;
    for (let j = 1; j <= Math.sqrt(i); j++) {
      let ans = 1 + dp[i - j * j];
      min = Math.min(ans, min);
    }
    dp[i] = min;
  }
  return dp[n];
};
```

