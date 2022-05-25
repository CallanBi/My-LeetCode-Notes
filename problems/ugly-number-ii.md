
# 264. Ugly Number II - 丑数 II

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Hash Table-哈希表-blue.svg">   <img src="https://img.shields.io/badge/Math-数学-blue.svg">   <img src="https://img.shields.io/badge/Dynamic Programming-动态规划-blue.svg">   <img src="https://img.shields.io/badge/Heap (Priority Queue)-堆（优先队列）-blue.svg">  


## Description - 题目描述

### EN:
<p>An <strong>ugly number</strong> is a positive integer whose prime factors are limited to <code>2</code>, <code>3</code>, and <code>5</code>.</p>

<p>Given an integer <code>n</code>, return <em>the</em> <code>n<sup>th</sup></code> <em><strong>ugly number</strong></em>.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>

<pre>
<strong>Input:</strong> n = 10
<strong>Output:</strong> 12
<strong>Explanation:</strong> [1, 2, 3, 4, 5, 6, 8, 9, 10, 12] is the sequence of the first 10 ugly numbers.
</pre>

<p><strong>Example 2:</strong></p>

<pre>
<strong>Input:</strong> n = 1
<strong>Output:</strong> 1
<strong>Explanation:</strong> 1 has no prime factors, therefore all of its prime factors are limited to 2, 3, and 5.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= n &lt;= 1690</code></li>
</ul>


### ZH-CN:
<p>给你一个整数 <code>n</code> ，请你找出并返回第 <code>n</code> 个 <strong>丑数</strong> 。</p>

<p><strong>丑数 </strong>就是只包含质因数 <code>2</code>、<code>3</code> 和/或 <code>5</code> 的正整数。</p>

<p> </p>

<p><strong>示例 1：</strong></p>

<pre>
<strong>输入：</strong>n = 10
<strong>输出：</strong>12
<strong>解释：</strong>[1, 2, 3, 4, 5, 6, 8, 9, 10, 12] 是由前 10 个丑数组成的序列。
</pre>

<p><strong>示例 2：</strong></p>

<pre>
<strong>输入：</strong>n = 1
<strong>输出：</strong>1
<strong>解释：</strong>1 通常被视为丑数。
</pre>

<p> </p>

<p><strong>提示：</strong></p>

<ul>
	<li><code>1 <= n <= 1690</code></li>
</ul>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/ugly-number-ii/description/)  -  [LeetCode-CN](https://leetcode.cn/problems/ugly-number-ii/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| typescript  | 76 ms | 45.8 MB | 2022/04/12 0:13 |

```typescript

function nthUglyNumber(n: number): number {
  const dp: number[] = [0, 1];

  if (n === 1) {
    return dp[n];
  }

  let p2 = 1, p3 = 1, p5 = 1;

  for (let i = 2; i <= n; i++) {
    dp[i] = Math.min(2 * dp[p2], 3 * dp[p3], 5 * dp[p5]);

    if (dp[i] === 2 * dp[p2]) {
      ++p2;
    }
    if (dp[i] === 3 * dp[p3]) {
      ++p3;
    }
    if (dp[i] === 5 * dp[p5]) {
      ++p5;
    }
  }

  return dp[n];
};

```
## My Notes - 我的笔记


与 剑指 Offer 49. 丑数 相同，可以去参考那边的笔记。


