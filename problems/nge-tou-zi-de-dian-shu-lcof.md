
# 剑指 Offer 60. n个骰子的点数  LCOF - n个骰子的点数

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Math-数学-blue.svg">   <img src="https://img.shields.io/badge/Dynamic Programming-动态规划-blue.svg">   <img src="https://img.shields.io/badge/Probability and Statistics-概率与统计-blue.svg">  


## Description - 题目描述

### EN:
English description is not available for the problem. Please switch to Chinese.

### ZH-CN:
<p>把n个骰子扔在地上，所有骰子朝上一面的点数之和为s。输入n，打印出s的所有可能的值出现的概率。</p>

<p>&nbsp;</p>

<p>你需要用一个浮点数数组返回答案，其中第 i 个元素代表这 n 个骰子所能掷出的点数集合中第 i 小的那个的概率。</p>

<p>&nbsp;</p>

<p><strong>示例 1:</strong></p>

<pre><strong>输入:</strong> 1
<strong>输出:</strong> [0.16667,0.16667,0.16667,0.16667,0.16667,0.16667]
</pre>

<p><strong>示例&nbsp;2:</strong></p>

<pre><strong>输入:</strong> 2
<strong>输出:</strong> [0.02778,0.05556,0.08333,0.11111,0.13889,0.16667,0.13889,0.11111,0.08333,0.05556,0.02778]</pre>

<p>&nbsp;</p>

<p><strong>限制：</strong></p>

<p><code>1 &lt;= n &lt;= 11</code></p>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/nge-tou-zi-de-dian-shu-lcof/description/)  -  [LeetCode-CN](https://leetcode.cn/problems/nge-tou-zi-de-dian-shu-lcof/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| typescript  | 60 ms | 43.7 MB | 2022/04/26 19:14 |

```typescript

function dicesProbability(n: number): number[] {
  if (n === 1) {
    return new Array(6).fill(1 / 6);
  }

  const dp: number[][] = new Array(n + 1).fill([]).map(i => new Array(6 * n + 1).fill(0))

  const base: number = 1 / 6;

  for (let i = 1; i <= 6; i++) {
    dp[1][i] = base;
  }

  for (let i = 2; i < dp.length; i++) {
    for (let j = 6 * i; j >= i; j--) {
      for (let k = 1; k <= 6 && j - k >= 1; k++) {
        dp[i][j] += dp[i - 1][j - k] * base;
      }
    }
  }

  return dp[n].slice(n);

};

```
## My Notes - 我的笔记


动态规划的应用。

设 $f(i, j)$ 是骰子个数为 $i$，点数和为 $j$ 时的概率。

对于每一个$i$，$j$ 的取值范围为 $[i, 6i]$。

状态转移方程：$f(i, j) = [ f(i-1, j-1) + f(i-1, j-2) + ... + f(i, j - 6) ]* 1 / 6$。

故可以初始化`dp[1][1]` ~ `dp[1][6]` 都为 $1 / 6$。

```typescript
function dicesProbability(n: number): number[] {
  if (n === 1) {
    return new Array(6).fill(1 / 6);
  }

  const dp: number[][] = new Array(n + 1).fill([]).map(i => new Array(6 * n + 1).fill(0))

  const base: number = 1 / 6;

  for (let i = 1; i <= 6; i++) {
    dp[1][i] = base;
  }

  for (let i = 2; i < dp.length; i++) {
    for (let j = 6 * i; j >= i; j--) {
      for (let k = 1; k <= 6 && j - k >= 1; k++) {
        dp[i][j] += dp[i - 1][j - k] * base;
      }
    }
  }

  return dp[n].slice(n);

};
```




