
# 剑指 Offer 14- I. 剪绳子  LCOF - 剪绳子

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Math-数学-blue.svg">   <img src="https://img.shields.io/badge/Dynamic Programming-动态规划-blue.svg">  


## Description - 题目描述

### EN:
English description is not available for the problem. Please switch to Chinese.

### ZH-CN:
<p>给你一根长度为 <code>n</code> 的绳子，请把绳子剪成整数长度的 <code>m</code> 段（m、n都是整数，n&gt;1并且m&gt;1），每段绳子的长度记为 <code>k[0],k[1]...k[m-1]</code> 。请问 <code>k[0]*k[1]*...*k[m-1]</code> 可能的最大乘积是多少？例如，当绳子的长度是8时，我们把它剪成长度分别为2、3、3的三段，此时得到的最大乘积是18。</p>

<p><strong>示例 1：</strong></p>

<pre><strong>输入: </strong>2
<strong>输出: </strong>1
<strong>解释: </strong>2 = 1 + 1, 1 &times; 1 = 1</pre>

<p><strong>示例&nbsp;2:</strong></p>

<pre><strong>输入: </strong>10
<strong>输出: </strong>36
<strong>解释: </strong>10 = 3 + 3 + 4, 3 &times;&nbsp;3 &times;&nbsp;4 = 36</pre>

<p><strong>提示：</strong></p>

<ul>
	<li><code>2 &lt;= n &lt;= 58</code></li>
</ul>

<p>注意：本题与主站 343 题相同：<a href="https://leetcode-cn.com/problems/integer-break/">https://leetcode-cn.com/problems/integer-break/</a></p>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/jian-sheng-zi-lcof/description/)  -  [LeetCode-CN](https://leetcode.cn/problems/jian-sheng-zi-lcof/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| typescript  | 92 ms | 40.3 MB | 2021/04/17 16:59 |

```typescript

function cuttingRope(n: number): number {
  const dp = new Array<number>(n).fill(0);
  dp[0] = 1;
  dp[1] = 1;
  dp[2] = 2;
  dp[3] = 3;

  if (n <= 3) {
    return dp[n-1];
  }

  for (let i = 4; i <= n; ++i) {
    let max = -1;
    for (let j = 0; j < i; ++j) {
      const curRes = dp[j] * dp[i - j];
      if (curRes > max) {
        max = curRes;
      }
    }
    dp[i] = max;
  }
  return dp[n];
};

```
## My Notes - 我的笔记


与主站 [343 题](https://leetcode-cn.com/problems/integer-break/) 相同

思路：

$ dp(i+1)=max \{ dp(i)1, dp(i-1)dp(2),...,dp(2)dp(i-1),dp(1)(i)) \}  $


