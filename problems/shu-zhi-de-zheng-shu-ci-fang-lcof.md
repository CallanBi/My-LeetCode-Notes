
# 剑指 Offer 16. 数值的整数次方 LCOF - 数值的整数次方

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Recursion-递归-blue.svg">   <img src="https://img.shields.io/badge/Math-数学-blue.svg">  


## Description - 题目描述

### EN:
English description is not available for the problem. Please switch to Chinese.

### ZH-CN:
<p>实现 <a href="https://www.cplusplus.com/reference/valarray/pow/">pow(<em>x</em>, <em>n</em>)</a> ，即计算 x 的 n 次幂函数（即，x<sup>n</sup>）。不得使用库函数，同时不需要考虑大数问题。</p>

<p> </p>

<p><strong>示例 1：</strong></p>

<pre>
<strong>输入：</strong>x = 2.00000, n = 10
<strong>输出：</strong>1024.00000
</pre>

<p><strong>示例 2：</strong></p>

<pre>
<strong>输入：</strong>x = 2.10000, n = 3
<strong>输出：</strong>9.26100</pre>

<p><strong>示例 3：</strong></p>

<pre>
<strong>输入：</strong>x = 2.00000, n = -2
<strong>输出：</strong>0.25000
<strong>解释：</strong>2<sup>-2</sup> = 1/2<sup>2</sup> = 1/4 = 0.25</pre>

<p> </p>

<p><strong>提示：</strong></p>

<ul>
	<li><code>-100.0 < x < 100.0</code></li>
	<li><code>-2<sup>31</sup> <= n <= 2<sup>31</sup>-1</code></li>
	<li><code>-10<sup>4</sup> <= x<sup>n</sup> <= 10<sup>4</sup></code></li>
</ul>

<p> </p>

<p>注意：本题与主站 50 题相同：<a href="https://leetcode-cn.com/problems/powx-n/">https://leetcode-cn.com/problems/powx-n/</a></p>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/shu-zhi-de-zheng-shu-ci-fang-lcof/description/)  -  [LeetCode-CN](https://leetcode.cn/problems/shu-zhi-de-zheng-shu-ci-fang-lcof/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| typescript  | 80 ms | 39.4 MB | 2021/10/10 23:48 |

```typescript

function myPow(x: number, n: number): number {
    if (n === 0) {
        return 1;
    }
    if (n === -1) {
        return 1/x;
    }

    if (n & 1) {
        // n 为奇数
        // 即 a^(n-1) * a
        return myPow(x*x, n >> 1) * x;
    } else {
        // n 为偶数
        return myPow(x*x, n >> 1);
    }

};

```
## My Notes - 我的笔记


No notes

