
# 剑指 Offer 57 - II. 和为s的连续正数序列 LCOF - 和为s的连续正数序列

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Math-数学-blue.svg">   <img src="https://img.shields.io/badge/Two Pointers-双指针-blue.svg">   <img src="https://img.shields.io/badge/Enumeration-枚举-blue.svg">  


## Description - 题目描述

### EN:
<p>English description is not available for the problem. Please switch to Chinese.</p>


### ZH-CN:
<p>输入一个正整数 <code>target</code> ，输出所有和为 <code>target</code> 的连续正整数序列（至少含有两个数）。</p>

<p>序列内的数字由小到大排列，不同序列按照首个数字从小到大排列。</p>

<p>&nbsp;</p>

<p><strong>示例 1：</strong></p>

<pre><strong>输入：</strong>target = 9
<strong>输出：</strong>[[2,3,4],[4,5]]
</pre>

<p><strong>示例 2：</strong></p>

<pre><strong>输入：</strong>target = 15
<strong>输出：</strong>[[1,2,3,4,5],[4,5,6],[7,8]]
</pre>

<p>&nbsp;</p>

<p><strong>限制：</strong></p>

<ul>
	<li><code>1 &lt;= target &lt;= 10^5</code></li>
</ul>

<p>&nbsp;</p>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/he-wei-sde-lian-xu-zheng-shu-xu-lie-lcof/description/)  -  [LeetCode-CN](https://leetcode.cn/problems/he-wei-sde-lian-xu-zheng-shu-xu-lie-lcof/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| typescript  | 112 ms | 48.2 MB | 2022/04/23 16:23 |

```typescript

function findContinuousSequence(target: number): number[][] {
  if (target === 1) {
    return [[1]];
  }

  const arr = new Array(target).fill(0).map((_, idx) => idx+1);

  const len = arr.length;

  let i = 0, j = 1, sum = 0, res: number[][] = [];

  sum = arr[0] + arr[1];

  while((j !== len || i !== len) && i < j) {
    if (sum > target && (j !== len || i !== len) && i < j) {
      sum -= arr[i];
      i++;
    } else if (sum < target && (j !== len || i !== len) && i < j) {
      j++;
      sum += arr[j];
    } 
    
    if (sum === target && i < j) {
      res.push(arr.slice(i, j+1));
      j++;
      sum += arr[j];
    }
  }
  
  return res;
};

```
## My Notes - 我的笔记


用双指针的思路做滑动窗口。

注意：从第一个数和第二个数开始滑动

```typescript
function findContinuousSequence(target: number): number[][] {
  if (target === 1) {
    return [[1]];
  }

  const arr = new Array(target).fill(0).map((_, idx) => idx+1);

  const len = arr.length;

  let i = 0, j = 1, sum = 0, res: number[][] = [];

  sum = arr[0] + arr[1];

  while((j !== len || i !== len) && i < j) {
    if (sum > target && (j !== len || i !== len) && i < j) {
      sum -= arr[i];
      i++;
    } else if (sum < target && (j !== len || i !== len) && i < j) {
      j++;
      sum += arr[j];
    } 
    
    if (sum === target && i < j) {
      res.push(arr.slice(i, j+1));
      j++;
      sum += arr[j];
    }
  }
  
  return res;
};
```

