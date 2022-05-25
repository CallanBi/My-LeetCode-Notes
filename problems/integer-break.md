
# 343. Integer Break - 整数拆分

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Math-数学-blue.svg">   <img src="https://img.shields.io/badge/Dynamic Programming-动态规划-blue.svg">  


## Description - 题目描述

### EN:
<p>Given an integer <code>n</code>, break it into the sum of <code>k</code> <strong>positive integers</strong>, where <code>k &gt;= 2</code>, and maximize the product of those integers.</p>

<p>Return <em>the maximum product you can get</em>.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>

<pre>
<strong>Input:</strong> n = 2
<strong>Output:</strong> 1
<strong>Explanation:</strong> 2 = 1 + 1, 1 &times; 1 = 1.
</pre>

<p><strong>Example 2:</strong></p>

<pre>
<strong>Input:</strong> n = 10
<strong>Output:</strong> 36
<strong>Explanation:</strong> 10 = 3 + 3 + 4, 3 &times; 3 &times; 4 = 36.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>2 &lt;= n &lt;= 58</code></li>
</ul>


### ZH-CN:
<p>给定一个正整数&nbsp;<code>n</code>&nbsp;，将其拆分为 <code>k</code> 个 <strong>正整数</strong> 的和（&nbsp;<code>k &gt;= 2</code>&nbsp;），并使这些整数的乘积最大化。</p>

<p>返回 <em>你可以获得的最大乘积</em>&nbsp;。</p>

<p>&nbsp;</p>

<p><strong>示例 1:</strong></p>

<pre>
<strong>输入: </strong>n = 2
<strong>输出: </strong>1
<strong>解释: </strong>2 = 1 + 1, 1 × 1 = 1。</pre>

<p><strong>示例&nbsp;2:</strong></p>

<pre>
<strong>输入: </strong>n = 10
<strong>输出: </strong>36
<strong>解释: </strong>10 = 3 + 3 + 4, 3 ×&nbsp;3 ×&nbsp;4 = 36。</pre>

<p>&nbsp;</p>

<p><strong>提示:</strong></p>

<ul>
	<li><code>2 &lt;= n &lt;= 58</code></li>
</ul>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/integer-break/description/)  -  [LeetCode-CN](https://leetcode.cn/problems/integer-break/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| typescript  | 72 ms | 42.5 MB | 2022/04/10 21:16 |

```typescript

function integerBreak(n: number): number {
  if (n === 2) {
    return 1;
  }
  if (n === 3) {
    return 2;
  }
  const dp: number[] = [];
  dp[0] = 0;
  dp[1] = 0;
  dp[2] = 2;
  dp[3] = 3;

  for (let i = 2; i <= n; i++) {
    for (let j = 2; j <= i / 2; j++) {
      dp[i] = Math.max((dp[j] ?? 0) * (dp[i-j] ?? 0), (dp[i] ?? 0));
    }
  }
  return dp[n];
};

```
## My Notes - 我的笔记


与 剑指 Offer 14- I. 剪绳子 一样。

思路：

$dp(i+1)=max \{ dp(i)1, dp(i-1)dp(2),...,dp(2)dp(i-1),dp(1)(i)) \} $


