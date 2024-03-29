
# 剑指 Offer 39. 数组中出现次数超过一半的数字  LCOF - 数组中出现次数超过一半的数字

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Array-数组-blue.svg">   <img src="https://img.shields.io/badge/Hash Table-哈希表-blue.svg">   <img src="https://img.shields.io/badge/Divide and Conquer-分治-blue.svg">   <img src="https://img.shields.io/badge/Counting-计数-blue.svg">   <img src="https://img.shields.io/badge/Sorting-排序-blue.svg">  


## Description - 题目描述

### EN:
English description is not available for the problem. Please switch to Chinese.

### ZH-CN:
<p>数组中有一个数字出现的次数超过数组长度的一半，请找出这个数字。</p>

<p>&nbsp;</p>

<p>你可以假设数组是非空的，并且给定的数组总是存在多数元素。</p>

<p>&nbsp;</p>

<p><strong>示例&nbsp;1:</strong></p>

<pre><strong>输入:</strong> [1, 2, 3, 2, 2, 2, 5, 4, 2]
<strong>输出:</strong> 2</pre>

<p>&nbsp;</p>

<p><strong>限制：</strong></p>

<p><code>1 &lt;= 数组长度 &lt;= 50000</code></p>

<p>&nbsp;</p>

<p>注意：本题与主站 169 题相同：<a href="https://leetcode-cn.com/problems/majority-element/">https://leetcode-cn.com/problems/majority-element/</a></p>

<p>&nbsp;</p>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/shu-zu-zhong-chu-xian-ci-shu-chao-guo-yi-ban-de-shu-zi-lcof/description/)  -  [LeetCode-CN](https://leetcode.cn/problems/shu-zu-zhong-chu-xian-ci-shu-chao-guo-yi-ban-de-shu-zi-lcof/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| typescript  | 76 ms | 41.3 MB | 2021/11/10 20:31 |

```typescript

function majorityElement(nums: number[]): number {
  let candidate = 0, count = 0;
  for (let i of nums) {
    if (count === 0) {
      candidate = i;
    }
    count += i === candidate ? 1 : -1;
  }
  return candidate;
};

```
## My Notes - 我的笔记


直接用摩尔投票算法找众数：
```typescript
function majorityElement(nums: number[]): number {
  let candidate = 0, count = 0;
  for (let i of nums) {
    if (count === 0) {
      candidate = i;
    }
    count += i === candidate ? 1 : -1;
  }
  return candidate;
};
```

