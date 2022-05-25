
# 剑指 Offer 57. 和为s的两个数字 LCOF - 和为s的两个数字

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Array-数组-blue.svg">   <img src="https://img.shields.io/badge/Two Pointers-双指针-blue.svg">   <img src="https://img.shields.io/badge/Binary Search-二分查找-blue.svg">  


## Description - 题目描述

### EN:
<p>English description is not available for the problem. Please switch to Chinese.</p>


### ZH-CN:
<p>输入一个递增排序的数组和一个数字s，在数组中查找两个数，使得它们的和正好是s。如果有多对数字的和等于s，则输出任意一对即可。</p>

<p>&nbsp;</p>

<p><strong>示例 1：</strong></p>

<pre><strong>输入：</strong>nums = [2,7,11,15], target = 9
<strong>输出：</strong>[2,7] 或者 [7,2]
</pre>

<p><strong>示例 2：</strong></p>

<pre><strong>输入：</strong>nums = [10,26,30,31,47,60], target = 40
<strong>输出：</strong>[10,30] 或者 [30,10]
</pre>

<p>&nbsp;</p>

<p><strong>限制：</strong></p>

<ul>
	<li><code>1 &lt;= nums.length &lt;= 10^5</code></li>
	<li><code>1 &lt;= nums[i]&nbsp;&lt;= 10^6</code></li>
</ul>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/he-wei-sde-liang-ge-shu-zi-lcof/description/)  -  [LeetCode-CN](https://leetcode.cn/problems/he-wei-sde-liang-ge-shu-zi-lcof/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| typescript  | 92 ms | 57 MB | 2022/04/22 23:19 |

```typescript

function twoSum(nums: number[], target: number): number[] {
  if (nums.length === 1) {
    return nums;
  }

  let i = 0, j = nums.length - 1;

  while (i < j) {
    if (nums[i] + nums[j] > target && i < j) {
      j--;
    } else if (nums[i] + nums[j] < target && i < j) {
      i++;
    } else if (nums[i] + nums[j] === target) {
      return [nums[i], nums[j]];
    }
  }

  return [];
};

```
## My Notes - 我的笔记


排序数组，双指针法即可。

