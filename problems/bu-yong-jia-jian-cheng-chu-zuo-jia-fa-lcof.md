
# 剑指 Offer 65. 不用加减乘除做加法 LCOF - 不用加减乘除做加法

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Bit Manipulation-位运算-blue.svg">   <img src="https://img.shields.io/badge/Math-数学-blue.svg">  


## Description - 题目描述

### EN:
English description is not available for the problem. Please switch to Chinese.

### ZH-CN:
<p>写一个函数，求两个整数之和，要求在函数体内不得使用 &ldquo;+&rdquo;、&ldquo;-&rdquo;、&ldquo;*&rdquo;、&ldquo;/&rdquo; 四则运算符号。</p>

<p>&nbsp;</p>

<p><strong>示例:</strong></p>

<pre><strong>输入:</strong> a = 1, b = 1
<strong>输出:</strong> 2</pre>

<p>&nbsp;</p>

<p><strong>提示：</strong></p>

<ul>
	<li><code>a</code>,&nbsp;<code>b</code>&nbsp;均可能是负数或 0</li>
	<li>结果不会溢出 32 位整数</li>
</ul>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/bu-yong-jia-jian-cheng-chu-zuo-jia-fa-lcof/description/)  -  [LeetCode-CN](https://leetcode.cn/problems/bu-yong-jia-jian-cheng-chu-zuo-jia-fa-lcof/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| typescript  | 64 ms | 42.1 MB | 2022/04/30 13:24 |

```typescript

function add(a: number, b: number): number {
  let sum = 0, carry = 0;

  let aCopied = a, bCopied = b;

  do {
    sum = aCopied ^ bCopied;
    carry = (aCopied & bCopied) << 1;
    aCopied = sum;
    bCopied = carry;
  }
  while (bCopied !== 0);

  return aCopied;
};

```
## My Notes - 我的笔记


用位运算实现加法。
思路：求非进位和和进位，相加，直到进位为0为止。
```typescript
function add(a: number, b: number): number {
  let sum = 0, carry = 0;

  let aCopied = a, bCopied = b;

  do {
    sum = aCopied ^ bCopied;
    carry = (aCopied & bCopied) << 1;
    aCopied = sum;
    bCopied = carry;
  }
  while (bCopied !== 0);

  return aCopied;
};
```

