
# 剑指 Offer 10- II. 青蛙跳台阶问题  LCOF - 青蛙跳台阶问题

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Memoization-记忆化搜索-blue.svg">   <img src="https://img.shields.io/badge/Math-数学-blue.svg">   <img src="https://img.shields.io/badge/Dynamic Programming-动态规划-blue.svg">  


## Description - 题目描述

### EN:
English description is not available for the problem. Please switch to Chinese.

### ZH-CN:
<p>一只青蛙一次可以跳上1级台阶，也可以跳上2级台阶。求该青蛙跳上一个 <code>n</code>&nbsp;级的台阶总共有多少种跳法。</p>

<p>答案需要取模 1e9+7（1000000007），如计算初始结果为：1000000008，请返回 1。</p>

<p><strong>示例 1：</strong></p>

<pre><strong>输入：</strong>n = 2
<strong>输出：</strong>2
</pre>

<p><strong>示例 2：</strong></p>

<pre><strong>输入：</strong>n = 7
<strong>输出：</strong>21
</pre>

<p><strong>示例 3：</strong></p>

<pre><strong>输入：</strong>n = 0
<strong>输出：</strong>1</pre>

<p><strong>提示：</strong></p>

<ul>
	<li><code>0 &lt;= n &lt;= 100</code></li>
</ul>

<p>注意：本题与主站 70 题相同：<a href="https://leetcode-cn.com/problems/climbing-stairs/">https://leetcode-cn.com/problems/climbing-stairs/</a></p>

<p>&nbsp;</p>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/qing-wa-tiao-tai-jie-wen-ti-lcof/description/)  -  [LeetCode-CN](https://leetcode-cn.com/problems/qing-wa-tiao-tai-jie-wen-ti-lcof/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| typescript  | 88 ms | 39.4 MB | 2021/04/04 21:17 |

```typescript

function numWays(n: number): number {
  const dp: bigint[] = [];
  dp[0] = 1n;
  dp[1] = 1n;
  dp[2] = 2n;

  if (n <= 2) {
    return Number(dp[n]);
  }

  for (let i = 3; i <= n; i++) {
    dp[i] = dp[i-1] + dp[i-2];
  }

  return Number(dp[n] % 1000000007n);
};

```
## My Notes - 我的笔记


`f(1) = 1, f(2) = 2`
跳 n级台阶，可以有两种情况：
1. 先上了一级台阶，后 n 级有 `f(n-1)` 种方法；
2. 先上了二级台阶，后 n 级有`f(n-2)` 种方法；

建立状态转移方程，用 dp的思想去解决

