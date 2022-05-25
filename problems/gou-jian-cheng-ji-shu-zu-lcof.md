
# 剑指 Offer 66. 构建乘积数组 LCOF - 构建乘积数组

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Array-数组-blue.svg">   <img src="https://img.shields.io/badge/Prefix Sum-前缀和-blue.svg">  


## Description - 题目描述

### EN:
English description is not available for the problem. Please switch to Chinese.

### ZH-CN:
<p>给定一个数组 <code>A[0,1,…,n-1]</code>，请构建一个数组 <code>B[0,1,…,n-1]</code>，其中 <code>B[i]</code> 的值是数组 <code>A</code> 中除了下标 <code>i</code> 以外的元素的积, 即 <code>B[i]=A[0]×A[1]×…×A[i-1]×A[i+1]×…×A[n-1]</code>。不能使用除法。</p>

<p> </p>

<p><strong>示例:</strong></p>

<pre>
<strong>输入:</strong> [1,2,3,4,5]
<strong>输出:</strong> [120,60,40,30,24]</pre>

<p> </p>

<p><strong>提示：</strong></p>

<ul>
	<li>所有元素乘积之和不会溢出 32 位整数</li>
	<li><code>a.length <= 100000</code></li>
</ul>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/gou-jian-cheng-ji-shu-zu-lcof/description/)  -  [LeetCode-CN](https://leetcode-cn.com/problems/gou-jian-cheng-ji-shu-zu-lcof/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| typescript  | 96 ms | 61.4 MB | 2022/04/30 15:08 |

```typescript

function constructArr(a: number[]): number[] {
  if (a.length === 0) {
    return [];
  }

  if (a.length === 1) {
    return [0];
  }

  let leftMem: number[] = [a[0]], rightMem: number[] = new Array(a.length);

  rightMem[a.length - 1] = a[a.length - 1];


  for (let i = 1; i < a.length; i++) {
    leftMem[i] = a[i] * leftMem[i - 1];
  }

  for (let j = a.length - 2; j >= 0; j--) {
    rightMem[j] = a[j] * rightMem[j + 1];
  }

  return a.map((_, idx) => (leftMem[idx - 1] ?? 1) * (rightMem[idx + 1] ?? 1));


};

```
## My Notes - 我的笔记


$O(n^2)$的方法：

```typescript
function constructArr(a: number[]): number[] {
  return a.map((_, idx) => {
    return [...a.slice(0, idx), ...a.slice(idx + 1)].reduce((acc, cur) => acc * cur, 1);
  });
};
```

$O(n)$ 的方法：

先从左到右遍历一遍乘积为 `leftMem`，再从右到左遍历一遍乘积为`rightMem`，存储起来，再遍历一遍数组返回 `leftMem[i-1] * rightMem[i+1]` 即可。

```typescript
function constructArr(a: number[]): number[] {
  if (a.length === 0) {
    return [];
  }

  if (a.length === 1) {
    return [0];
  }

  let leftMem: number[] = [a[0]], rightMem: number[] = new Array(a.length);

  rightMem[a.length - 1] = a[a.length - 1];


  for (let i = 1; i < a.length; i++) {
    leftMem[i] = a[i] * leftMem[i - 1];
  }

  for (let j = a.length - 2; j >= 0; j--) {
    rightMem[j] = a[j] * rightMem[j + 1];
  }

  return a.map((_, idx) => (leftMem[idx - 1] ?? 1) * (rightMem[idx + 1] ?? 1));
};
```


