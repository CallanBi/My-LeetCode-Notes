
# 剑指 Offer 45. 把数组排成最小的数 LCOF - 把数组排成最小的数

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Greedy-贪心-blue.svg">   <img src="https://img.shields.io/badge/String-字符串-blue.svg">   <img src="https://img.shields.io/badge/Sorting-排序-blue.svg">  


## Description - 题目描述

### EN:
English description is not available for the problem. Please switch to Chinese.

### ZH-CN:
<p>输入一个非负整数数组，把数组里所有数字拼接起来排成一个数，打印能拼接出的所有数字中最小的一个。</p>

<p>&nbsp;</p>

<p><strong>示例 1:</strong></p>

<pre><strong>输入:</strong> <code>[10,2]</code>
<strong>输出:</strong> &quot;<code>102&quot;</code></pre>

<p><strong>示例&nbsp;2:</strong></p>

<pre><strong>输入:</strong> <code>[3,30,34,5,9]</code>
<strong>输出:</strong> &quot;<code>3033459&quot;</code></pre>

<p>&nbsp;</p>

<p><strong>提示:</strong></p>

<ul>
	<li><code>0 &lt; nums.length &lt;= 100</code></li>
</ul>

<p><strong>说明: </strong></p>

<ul>
	<li>输出结果可能非常大，所以你需要返回一个字符串而不是整数</li>
	<li>拼接起来的数字可能会有前导 0，最后结果不需要去掉前导 0</li>
</ul>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/ba-shu-zu-pai-cheng-zui-xiao-de-shu-lcof/description/)  -  [LeetCode-CN](https://leetcode.cn/problems/ba-shu-zu-pai-cheng-zui-xiao-de-shu-lcof/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| typescript  | 88 ms | 39.5 MB | 2021/12/17 21:35 |

```typescript

function minNumber(nums: number[]): string {
  return nums.sort((a, b) => Number(String(a) + String(b)) < Number(String(b) + String(a)) ? -1 : 1).map(e => String(e)).join('');
};

```
## My Notes - 我的笔记


传入排序规则的匿名函数，用 `a + b  < b + a` 判断即可
```typescript
function minNumber(nums: number[]): string {
  return nums.sort((a, b) => Number(String(a) + String(b)) < Number(String(b) + String(a)) ? -1 : 1).map(e => String(e)).join('');
};
```

