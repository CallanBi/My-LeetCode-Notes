
# 剑指 Offer 53 - II. 缺失的数字  LCOF - 0～n-1中缺失的数字

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Bit Manipulation-位运算-blue.svg">   <img src="https://img.shields.io/badge/Array-数组-blue.svg">   <img src="https://img.shields.io/badge/Hash Table-哈希表-blue.svg">   <img src="https://img.shields.io/badge/Math-数学-blue.svg">   <img src="https://img.shields.io/badge/Binary Search-二分查找-blue.svg">  


## Description - 题目描述

### EN:
English description is not available for the problem. Please switch to Chinese.

### ZH-CN:
<p>一个长度为n-1的递增排序数组中的所有数字都是唯一的，并且每个数字都在范围0～n-1之内。在范围0～n-1内的n个数字中有且只有一个数字不在该数组中，请找出这个数字。</p>

<p>&nbsp;</p>

<p><strong>示例 1:</strong></p>

<pre><strong>输入:</strong> [0,1,3]
<strong>输出:</strong> 2
</pre>

<p><strong>示例&nbsp;2:</strong></p>

<pre><strong>输入:</strong> [0,1,2,3,4,5,6,7,9]
<strong>输出:</strong> 8</pre>

<p>&nbsp;</p>

<p><strong>限制：</strong></p>

<p><code>1 &lt;= 数组长度 &lt;= 10000</code></p>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/que-shi-de-shu-zi-lcof/description/)  -  [LeetCode-CN](https://leetcode.cn/problems/que-shi-de-shu-zi-lcof/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| typescript  | 76 ms | 40.4 MB | 2021/12/22 19:19 |

```typescript

function missingNumber(nums: number[]): number {
  return devide(nums, 0, nums.length-1);
};

function devide(nums: number[], start: number, end: number): number {
  if (start > end) {
    return end + 1;
  }
  const middleIdx = start + ~~((end - start) / 2);
  if (nums[middleIdx] !== middleIdx) {
    if (nums[middleIdx - 1] !== middleIdx - 1) {
      return devide(nums, start, middleIdx-1);
    } else if (nums[middleIdx - 1] === middleIdx - 1) {
      return middleIdx;
    }
  } else {
    return devide(nums, middleIdx+1, end);
  }
}

```
## My Notes - 我的笔记


二分法的应用。

注意举几个例子才能搞清的边界条件。如长度为4的数组，分别有哪些情况。

摘自剑指 offfer:
> 如果中间元素的值和下标相等，那么下一轮查找只需要查找右半边；如果中间元素的值和下标不相等，并且它前面一个元素和它的下标相等，这意味着这个中间数字正好是第一个值和下标不相等的元素，它的下标就是在数组中不存在的数字；如果中间元素的值和下标不相等，并且它前面一个元素和它的下标不相等，这意味着下一轮查找我们只需要在左半边查找即可。

```typescript
function missingNumber(nums: number[]): number {
  return devide(nums, 0, nums.length-1);
};

function devide(nums: number[], start: number, end: number): number {
  if (start > end) {
    return end + 1;
  }
  const middleIdx = start + ~~((end - start) / 2);
  if (nums[middleIdx] !== middleIdx) {
    if (nums[middleIdx - 1] !== middleIdx - 1) {
      return devide(nums, start, middleIdx-1);
    } else if (nums[middleIdx - 1] === middleIdx - 1) {
      return middleIdx;
    }
  } else {
    return devide(nums, middleIdx+1, end);
  }
}
```

