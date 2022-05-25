
# 357. Count Numbers with Unique Digits - 统计各位数字都不同的数字个数

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Math-数学-blue.svg">   <img src="https://img.shields.io/badge/Dynamic Programming-动态规划-blue.svg">   <img src="https://img.shields.io/badge/Backtracking-回溯-blue.svg">  


## Description - 题目描述

### EN:
<p>Given an integer <code>n</code>, return the count of all numbers with unique digits, <code>x</code>, where <code>0 &lt;= x &lt; 10<sup>n</sup></code>.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>

<pre>
<strong>Input:</strong> n = 2
<strong>Output:</strong> 91
<strong>Explanation:</strong> The answer should be the total numbers in the range of 0 &le; x &lt; 100, excluding 11,22,33,44,55,66,77,88,99
</pre>

<p><strong>Example 2:</strong></p>

<pre>
<strong>Input:</strong> n = 0
<strong>Output:</strong> 1
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>0 &lt;= n &lt;= 8</code></li>
</ul>


### ZH-CN:
给你一个整数 <code>n</code> ，统计并返回各位数字都不同的数字 <code>x</code> 的个数，其中 <code>0 &lt;= x &lt; 10<sup>n</sup></code><sup>&nbsp;</sup>。
<div class="original__bRMd">
<div>
<p>&nbsp;</p>

<p><strong>示例 1：</strong></p>

<pre>
<strong>输入：</strong>n = 2
<strong>输出：</strong>91
<strong>解释：</strong>答案应为除去 <code>11、22、33、44、55、66、77、88、99 </code>外，在 0 ≤ x &lt; 100 范围内的所有数字。 
</pre>

<p><strong>示例 2：</strong></p>

<pre>
<strong>输入：</strong>n = 0
<strong>输出：</strong>1
</pre>
</div>
</div>

<p>&nbsp;</p>

<p><strong>提示：</strong></p>

<ul>
	<li><code>0 &lt;= n &lt;= 8</code></li>
</ul>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/count-numbers-with-unique-digits/description/)  -  [LeetCode-CN](https://leetcode.cn/problems/count-numbers-with-unique-digits/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| typescript  | 68 ms | 42.2 MB | 2022/04/11 18:53 |

```typescript

function countNumbersWithUniqueDigits(n: number): number {
  if (n === 0) {
    return 1;
  }

  if (n === 1) {
    return 10;
  }

  let acc = 10, mul = 1;

  for (let i = 1; i < n; i++) {
    mul *= 9 - (i - 1);
    acc = 9 * mul + acc;
  }

  return acc;
};

```
## My Notes - 我的笔记


与官方思路一致，用排列原理。

考虑 0 ~ 999 中的重复数字。可以分为 0 ~ 99 中的重复数字，再加上 100 ~ 999 中的重复数字即可。

100 ~ 999 中的重复数字可以这样考虑：从 1xx ~ 9xx 共有 9 组，而 xx 中的每一位都可以从 0~9 中取互不相同的数字。相当于从 9 个互不相同的元素中任意取2个排成一列，即 $A_9^2$。有 9 组即 $9 \times A_9^2$;

最后，用 100 ~ 999 中的重复数字 0 ~ 99 中的重复数字即可得到 0 ~ 999 的重复数字。用动态规划的语言，状态转移方程为 $dp[i+1] = dp[i] + 9 \times A_9^i$。最后用一个 `acc` 变量替代动态规划求解即可。

```typescript
function countNumbersWithUniqueDigits(n: number): number {
  if (n === 0) {
    return 1;
  }

  if (n === 1) {
    return 10;
  }

  let acc = 10, mul = 1;

  for (let i = 1; i < n; i++) {
    mul *= 9 - (i - 1);
    acc = 9 * mul + acc;
  }

  return acc;
};
```


