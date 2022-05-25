
# 剑指 Offer 14- II. 剪绳子 II LCOF - 剪绳子 II

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Math-数学-blue.svg">   <img src="https://img.shields.io/badge/Dynamic Programming-动态规划-blue.svg">  


## Description - 题目描述

### EN:
English description is not available for the problem. Please switch to Chinese.

### ZH-CN:
<p>给你一根长度为 <code>n</code> 的绳子，请把绳子剪成整数长度的 <code>m</code>&nbsp;段（m、n都是整数，n&gt;1并且m&gt;1），每段绳子的长度记为 <code>k[0],k[1]...k[m - 1]</code> 。请问 <code>k[0]*k[1]*...*k[m - 1]</code> 可能的最大乘积是多少？例如，当绳子的长度是8时，我们把它剪成长度分别为2、3、3的三段，此时得到的最大乘积是18。</p>

<p>答案需要取模 1e9+7（1000000007），如计算初始结果为：1000000008，请返回 1。</p>

<p>&nbsp;</p>

<p><strong>示例 1：</strong></p>

<pre><strong>输入: </strong>2
<strong>输出: </strong>1
<strong>解释: </strong>2 = 1 + 1, 1 &times; 1 = 1</pre>

<p><strong>示例&nbsp;2:</strong></p>

<pre><strong>输入: </strong>10
<strong>输出: </strong>36
<strong>解释: </strong>10 = 3 + 3 + 4, 3 &times;&nbsp;3 &times;&nbsp;4 = 36</pre>

<p>&nbsp;</p>

<p><strong>提示：</strong></p>

<ul>
	<li><code>2 &lt;= n &lt;= 1000</code></li>
</ul>

<p>注意：本题与主站 343 题相同：<a href="https://leetcode-cn.com/problems/integer-break/">https://leetcode-cn.com/problems/integer-break/</a></p>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/jian-sheng-zi-ii-lcof/description/)  -  [LeetCode-CN](https://leetcode.cn/problems/jian-sheng-zi-ii-lcof/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| javascript  | 212 ms | 43.6 MB | 2021/04/10 18:16 |

```javascript

/**
 * @param {number} n
 * @return {number}
 */
var cuttingRope = function(n) {
 const dp = new Array(n).fill(0n);
  dp[0] = 1n;
  dp[1] = 1n;
  dp[2] = 2n;
  dp[3] = 3n;
  if (n <= 3) {
    return dp[n-1];
  }
  for (let i = 4; i <= n; ++i) {
    // const maxArr = dp.slice(1, i).map((m, idx, arr) => m * arr[arr.length - 1 - idx]);
    let max = 0;
    for(let j = 1; j <= i/2; ++j) {
      const cur = dp[j] * dp[i - j];
      if (cur > max) {
        max = cur;
      }
    }
    dp[i] = max;
  }
  return Number(BigInt(dp[n]) % 1000000007n);
};

```
## My Notes - 我的笔记


还是用动态规划的方法吧
i 要从4开始，因为省略了特殊情况
取最大，可以从 i/2结束

