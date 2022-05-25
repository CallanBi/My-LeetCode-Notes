
# 剑指 Offer 17. 打印从1到最大的n位数 LCOF - 打印从1到最大的n位数

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Array-数组-blue.svg">   <img src="https://img.shields.io/badge/Math-数学-blue.svg">  


## Description - 题目描述

### EN:
English description is not available for the problem. Please switch to Chinese.

### ZH-CN:
<p>输入数字 <code>n</code>，按顺序打印出从 1 到最大的 n 位十进制数。比如输入 3，则打印出 1、2、3 一直到最大的 3 位数 999。</p>

<p><strong>示例 1:</strong></p>

<pre><strong>输入:</strong> n = 1
<strong>输出:</strong> [1,2,3,4,5,6,7,8,9]
</pre>

<p>&nbsp;</p>

<p>说明：</p>

<ul>
	<li>用返回一个整数列表来代替打印</li>
	<li>n 为正整数</li>
</ul>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/da-yin-cong-1dao-zui-da-de-nwei-shu-lcof/description/)  -  [LeetCode-CN](https://leetcode.cn/problems/da-yin-cong-1dao-zui-da-de-nwei-shu-lcof/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| typescript  | 132 ms | 49.4 MB | 2021/05/01 16:21 |

```typescript

function printNumbers(n: number): number[] {
    const res = [];
    for (let i = 1; i < Math.pow(10, n); i++) {
        res.push(i);
    }
    return res;
};

```
## My Notes - 我的笔记


根据题意不用考虑大数问题：
```javascript
function printNumbers(n: number): number[] {
    const res = [];
    for (let i = 1; i < Math.pow(10, n); i++) {
        res.push(i);
    }
    return res;
};
```

