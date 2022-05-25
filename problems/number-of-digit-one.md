
# 233. Number of Digit One - 数字 1 的个数

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Recursion-递归-blue.svg">   <img src="https://img.shields.io/badge/Math-数学-blue.svg">   <img src="https://img.shields.io/badge/Dynamic Programming-动态规划-blue.svg">  


## Description - 题目描述

### EN:
<p>Given an integer <code>n</code>, count <em>the total number of digit </em><code>1</code><em> appearing in all non-negative integers less than or equal to</em> <code>n</code>.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>

<pre>
<strong>Input:</strong> n = 13
<strong>Output:</strong> 6
</pre>

<p><strong>Example 2:</strong></p>

<pre>
<strong>Input:</strong> n = 0
<strong>Output:</strong> 0
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>0 &lt;= n &lt;= 10<sup>9</sup></code></li>
</ul>


### ZH-CN:
<p>给定一个整数 <code>n</code>，计算所有小于等于 <code>n</code> 的非负整数中数字 <code>1</code> 出现的个数。</p>

<p>&nbsp;</p>

<p><strong>示例 1：</strong></p>

<pre>
<strong>输入：</strong>n = 13
<strong>输出：</strong>6
</pre>

<p><strong>示例 2：</strong></p>

<pre>
<strong>输入：</strong>n = 0
<strong>输出：</strong>0
</pre>

<p>&nbsp;</p>

<p><strong>提示：</strong></p>

<ul>
	<li><code>0 &lt;= n &lt;= 10<sup>9</sup></code></li>
</ul>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/number-of-digit-one/description/)  -  [LeetCode-CN](https://leetcode.cn/problems/number-of-digit-one/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| typescript  | 56 ms | 42.3 MB | 2022/04/11 16:30 |

```typescript

function countDigitOne(n: number): number {
  const numArr = n.toString().split('').reverse();
  const dp1: number[] = [];
  const dp2: number[] = [];

  dp1[0] = 1;

  dp2[0] = numArr[0] === '0' ? 0 : 1;

  for (let i = 1; i < numArr.length; i++) {
    dp1[i] = 10 * dp1[i-1] + Math.pow(10, i);

    if (numArr[i] === '0') {
      dp2[i] = dp2[i-1];
    } else if (numArr[i] === '1') {
      const rest = Number(numArr.slice(0, i).reverse().join('')) + 1;
      dp2[i] = dp2[i-1] + rest + dp1[i-1];
    } else {
      dp2[i] = (Number(numArr[i])) * dp1[i-1] + Math.pow(10, i) + dp2[i-1];
    }
  }

  return dp2[numArr.length-1];
};

```
## My Notes - 我的笔记


与 剑指 Offer 43: 1～n 整数中 1 出现的次数 相同，解决方法应该是数位 dp 是最稳妥的。

可以去看看剑指 offer 的那道题的笔记。


