
# 剑指 Offer 10- I. 斐波那契数列  LCOF - 斐波那契数列

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Memoization-记忆化搜索-blue.svg">   <img src="https://img.shields.io/badge/Math-数学-blue.svg">   <img src="https://img.shields.io/badge/Dynamic Programming-动态规划-blue.svg">  


## Description - 题目描述

### EN:
English description is not available for the problem. Please switch to Chinese.

### ZH-CN:
<p>写一个函数，输入 <code>n</code> ，求斐波那契（Fibonacci）数列的第 <code>n</code> 项（即 <code>F(N)</code>）。斐波那契数列的定义如下：</p>

<pre>
F(0) = 0,   F(1) = 1
F(N) = F(N - 1) + F(N - 2), 其中 N > 1.</pre>

<p>斐波那契数列由 0 和 1 开始，之后的斐波那契数就是由之前的两数相加而得出。</p>

<p>答案需要取模 1e9+7（1000000007），如计算初始结果为：1000000008，请返回 1。</p>

<p> </p>

<p><strong>示例 1：</strong></p>

<pre>
<strong>输入：</strong>n = 2
<strong>输出：</strong>1
</pre>

<p><strong>示例 2：</strong></p>

<pre>
<strong>输入：</strong>n = 5
<strong>输出：</strong>5
</pre>

<p> </p>

<p><strong>提示：</strong></p>

<ul>
	<li><code>0 <= n <= 100</code></li>
</ul>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/fei-bo-na-qi-shu-lie-lcof/description/)  -  [LeetCode-CN](https://leetcode-cn.com/problems/fei-bo-na-qi-shu-lie-lcof/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| typescript  | 96 ms | 39.6 MB | 2021/04/04 20:42 |

```typescript

function fib(n: number): number {
  const result = [0, 1];
  if(n <= 1) {
    return result[n];
  }
  let fNMinus1: bigint = 1n;
  let fNMinus2: bigint = 0n;
  let fN: bigint = 0n;
  for (let i = 2; i <= n; i++) {
    fN = fNMinus1 + fNMinus2;
    fNMinus2 = fNMinus1;
    fNMinus1 = fN;
  }
  return Number(fN % (1000000007n));
};

```
## My Notes - 我的笔记


要注意顺序：
```
fNMinus2 = fNMinus1;
fNMinus1 = fN;
```
如果反过来，`f(n-1)` 和 `f(n-2)` 就相等了.

bigint：在数字后加/n，可以与 Number 互相转化

