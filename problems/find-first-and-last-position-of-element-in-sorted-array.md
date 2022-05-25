
# 34. Find First and Last Position of Element in Sorted Array - 在排序数组中查找元素的第一个和最后一个位置

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Array-数组-blue.svg">   <img src="https://img.shields.io/badge/Binary Search-二分查找-blue.svg">  


## Description - 题目描述

### EN:
<p>Given an array of integers <code>nums</code> sorted in non-decreasing order, find the starting and ending position of a given <code>target</code> value.</p>

<p>If <code>target</code> is not found in the array, return <code>[-1, -1]</code>.</p>

<p>You must&nbsp;write an algorithm with&nbsp;<code>O(log n)</code> runtime complexity.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>
<pre><strong>Input:</strong> nums = [5,7,7,8,8,10], target = 8
<strong>Output:</strong> [3,4]
</pre><p><strong>Example 2:</strong></p>
<pre><strong>Input:</strong> nums = [5,7,7,8,8,10], target = 6
<strong>Output:</strong> [-1,-1]
</pre><p><strong>Example 3:</strong></p>
<pre><strong>Input:</strong> nums = [], target = 0
<strong>Output:</strong> [-1,-1]
</pre>
<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>0 &lt;= nums.length &lt;= 10<sup>5</sup></code></li>
	<li><code>-10<sup>9</sup>&nbsp;&lt;= nums[i]&nbsp;&lt;= 10<sup>9</sup></code></li>
	<li><code>nums</code> is a non-decreasing array.</li>
	<li><code>-10<sup>9</sup>&nbsp;&lt;= target&nbsp;&lt;= 10<sup>9</sup></code></li>
</ul>


### ZH-CN:
<p>给定一个按照升序排列的整数数组 <code>nums</code>，和一个目标值 <code>target</code>。找出给定目标值在数组中的开始位置和结束位置。</p>

<p>如果数组中不存在目标值 <code>target</code>，返回 <code>[-1, -1]</code>。</p>

<p><strong>进阶：</strong></p>

<ul>
	<li>你可以设计并实现时间复杂度为 <code>O(log n)</code> 的算法解决此问题吗？</li>
</ul>

<p> </p>

<p><strong>示例 1：</strong></p>

<pre>
<strong>输入：</strong>nums = [<code>5,7,7,8,8,10]</code>, target = 8
<strong>输出：</strong>[3,4]</pre>

<p><strong>示例 2：</strong></p>

<pre>
<strong>输入：</strong>nums = [<code>5,7,7,8,8,10]</code>, target = 6
<strong>输出：</strong>[-1,-1]</pre>

<p><strong>示例 3：</strong></p>

<pre>
<strong>输入：</strong>nums = [], target = 0
<strong>输出：</strong>[-1,-1]</pre>

<p> </p>

<p><strong>提示：</strong></p>

<ul>
	<li><code>0 <= nums.length <= 10<sup>5</sup></code></li>
	<li><code>-10<sup>9</sup> <= nums[i] <= 10<sup>9</sup></code></li>
	<li><code>nums</code> 是一个非递减数组</li>
	<li><code>-10<sup>9</sup> <= target <= 10<sup>9</sup></code></li>
</ul>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/description/)  -  [LeetCode-CN](https://leetcode-cn.com/problems/find-first-and-last-position-of-element-in-sorted-array/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| typescript  | 64 ms | 42.9 MB | 2022/05/06 20:48 |

```typescript

function searchRange(nums: number[], target: number): number[] {
  return [searchFirst(nums, target), searchLast(nums, target)];
};


function searchFirst(nums: number[], target: number): number {
  if (nums.length === 0) {
    return -1;
  }
  if (nums.length === 1) {
    return nums[0] === target ? 0 : -1;
  }

  let i = 0, j = nums.length - 1, mid = Math.floor((i + j) / 2);

  while (i <= j) {
    mid = Math.floor((i + j) / 2);
    if (nums[mid] >= target) {
      j = mid - 1;
    } else {
      i = mid + 1;
    }
  }

  return (i >= nums.length || nums[i] !== target) ? -1 : i;
}

function searchLast(nums: number[], target: number): number {
  if (nums.length === 0) {
    return -1;
  }
  if (nums.length === 1) {
    return nums[0] === target ? 0 : -1;
  }

  let i = 0, j = nums.length - 1, mid = Math.floor((i + j) / 2);

  while (i <= j) {
    mid = Math.floor((i + j) / 2);
    if (nums[mid] > target) {
      j = mid - 1;
    } else {
      i = mid + 1;
    }
  }

  return (j < 0 || nums[j] !== target) ? -1 : j;
}

```
## My Notes - 我的笔记


参考：[【LeetCode】一个模板通杀所有「二分查找」问题](https://imageslr.com/2020/03/15/binary-search.html)

