
# 剑指 Offer 44. 数字序列中某一位的数字  LCOF - 数字序列中某一位的数字

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Math-数学-blue.svg">   <img src="https://img.shields.io/badge/Binary Search-二分查找-blue.svg">  


## Description - 题目描述

### EN:
English description is not available for the problem. Please switch to Chinese.

### ZH-CN:
<p>数字以0123456789101112131415&hellip;的格式序列化到一个字符序列中。在这个序列中，第5位（从下标0开始计数）是5，第13位是1，第19位是4，等等。</p>

<p>请写一个函数，求任意第n位对应的数字。</p>

<p>&nbsp;</p>

<p><strong>示例 1：</strong></p>

<pre><strong>输入：</strong>n = 3
<strong>输出：</strong>3
</pre>

<p><strong>示例 2：</strong></p>

<pre><strong>输入：</strong>n = 11
<strong>输出：</strong>0</pre>

<p>&nbsp;</p>

<p><strong>限制：</strong></p>

<ul>
	<li><code>0 &lt;= n &lt;&nbsp;2^31</code></li>
</ul>

<p>注意：本题与主站 400 题相同：<a href="https://leetcode-cn.com/problems/nth-digit/">https://leetcode-cn.com/problems/nth-digit/</a></p>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/shu-zi-xu-lie-zhong-mou-yi-wei-de-shu-zi-lcof/description/)  -  [LeetCode-CN](https://leetcode-cn.com/problems/shu-zi-xu-lie-zhong-mou-yi-wei-de-shu-zi-lcof/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| typescript  | 64 ms | 39.2 MB | 2021/12/17 20:58 |

```typescript

function findNthDigit(n: number): number {
  let placeDigit = 1, samePlaceLeftNum = 10 ** placeDigit, leftSeqNum = n;
  while (leftSeqNum > samePlaceLeftNum) {
    leftSeqNum -= samePlaceLeftNum;
    placeDigit++;
    samePlaceLeftNum = (10 ** placeDigit - 10 ** (placeDigit - 1)) * placeDigit;
  }
  if (placeDigit === 1) {
    return parseInt(String(n)[0]);
  }
  return parseInt(String(10 ** (placeDigit - 1) + (Math.floor(leftSeqNum / placeDigit)))[leftSeqNum % placeDigit]);
};

```
## My Notes - 我的笔记


# 最直观的方法，但会内存溢出
n 很大时会内存溢出。
```typescript
function findNthDigit(n: number): number {
  let str: string = '0';
  let counter = 0;
  while (str.length < n + 1) {
    counter++;
    str += String(counter);
  }
  return parseInt(str[n]);
};
```

# 用了剑指 offer 思路的代码，双 100%：
```typescript
function findNthDigit(n: number): number {
  let placeDigit = 1, samePlaceLeftNum = 10 ** placeDigit, leftSeqNum = n;
  while (leftSeqNum > samePlaceLeftNum) {
    leftSeqNum -= samePlaceLeftNum;
    placeDigit++;
    samePlaceLeftNum = (10 ** placeDigit - 10 ** (placeDigit - 1)) * placeDigit;
  }
  if (placeDigit === 1) {
    return parseInt(String(n)[0]);
  }
  return parseInt(String(10 ** (placeDigit - 1) + (Math.floor(leftSeqNum / placeDigit)))[leftSeqNum % placeDigit]);
};
```
思路参考剑指 offer 原文。

