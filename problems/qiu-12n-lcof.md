
# 剑指 Offer 64. 求1+2+…+n LCOF - 求1+2+…+n

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Bit Manipulation-位运算-blue.svg">   <img src="https://img.shields.io/badge/Recursion-递归-blue.svg">   <img src="https://img.shields.io/badge/Brainteaser-脑筋急转弯-blue.svg">  


## Description - 题目描述

### EN:
<p>English description is not available for the problem. Please switch to Chinese.</p>


### ZH-CN:
<p>求 <code>1+2+...+n</code> ，要求不能使用乘除法、for、while、if、else、switch、case等关键字及条件判断语句（A?B:C）。</p>

<p>&nbsp;</p>

<p><strong>示例 1：</strong></p>

<pre><strong>输入:</strong> n = 3
<strong>输出:&nbsp;</strong>6
</pre>

<p><strong>示例 2：</strong></p>

<pre><strong>输入:</strong> n = 9
<strong>输出:&nbsp;</strong>45
</pre>

<p>&nbsp;</p>

<p><strong>限制：</strong></p>

<ul>
	<li><code>1 &lt;= n&nbsp;&lt;= 10000</code></li>
</ul>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/qiu-12n-lcof/description/)  -  [LeetCode-CN](https://leetcode-cn.com/problems/qiu-12n-lcof/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| typescript  | 64 ms | 44 MB | 2022/04/30 12:53 |

```typescript

function sumNums(n: number): number {
  return new Array(n + 1).fill(0).reduce((acc, _, idx) => idx + acc, 0)
};

```
## My Notes - 我的笔记


ts/js 中可以用 `Array.Prototype.reduce`。

```typescript
function sumNums(n: number): number {
  return new Array(n + 1).fill(0).reduce((acc, _, idx) => idx + acc, 0)
};
```

