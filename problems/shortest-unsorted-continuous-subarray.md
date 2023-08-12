
# 581. Shortest Unsorted Continuous Subarray - 最短无序连续子数组

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Stack-栈-blue.svg">   <img src="https://img.shields.io/badge/Greedy-贪心-blue.svg">   <img src="https://img.shields.io/badge/Array-数组-blue.svg">   <img src="https://img.shields.io/badge/Two Pointers-双指针-blue.svg">   <img src="https://img.shields.io/badge/Sorting-排序-blue.svg">   <img src="https://img.shields.io/badge/Monotonic Stack-单调栈-blue.svg">  


## Description - 题目描述

### EN:
<p>Given an integer array <code>nums</code>, you need to find one <b>continuous subarray</b> such that if you only sort this subarray in non-decreasing order, then the whole array will be sorted in non-decreasing order.</p>

<p>Return <em>the shortest such subarray and output its length</em>.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input:</strong> nums = [2,6,4,8,10,9,15]
<strong>Output:</strong> 5
<strong>Explanation:</strong> You need to sort [6, 4, 8, 10, 9] in ascending order to make the whole array sorted in ascending order.
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre>
<strong>Input:</strong> nums = [1,2,3,4]
<strong>Output:</strong> 0
</pre>

<p><strong class="example">Example 3:</strong></p>

<pre>
<strong>Input:</strong> nums = [1]
<strong>Output:</strong> 0
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= nums.length &lt;= 10<sup>4</sup></code></li>
	<li><code>-10<sup>5</sup> &lt;= nums[i] &lt;= 10<sup>5</sup></code></li>
</ul>

<p>&nbsp;</p>
<strong>Follow up:</strong> Can you solve it in <code>O(n)</code> time complexity?

### ZH-CN:
<p>给你一个整数数组 <code>nums</code> ，你需要找出一个 <strong>连续子数组</strong> ，如果对这个子数组进行升序排序，那么整个数组都会变为升序排序。</p>

<p>请你找出符合题意的 <strong>最短</strong> 子数组，并输出它的长度。</p>

<p> </p>

<div class="original__bRMd">
<div>
<p><strong>示例 1：</strong></p>

<pre>
<strong>输入：</strong>nums = [2,6,4,8,10,9,15]
<strong>输出：</strong>5
<strong>解释：</strong>你只需要对 [6, 4, 8, 10, 9] 进行升序排序，那么整个表都会变为升序排序。
</pre>

<p><strong>示例 2：</strong></p>

<pre>
<strong>输入：</strong>nums = [1,2,3,4]
<strong>输出：</strong>0
</pre>

<p><strong>示例 3：</strong></p>

<pre>
<strong>输入：</strong>nums = [1]
<strong>输出：</strong>0
</pre>

<p> </p>

<p><strong>提示：</strong></p>

<ul>
	<li><code>1 <= nums.length <= 10<sup>4</sup></code></li>
	<li><code>-10<sup>5</sup> <= nums[i] <= 10<sup>5</sup></code></li>
</ul>

<p> </p>

<p><strong>进阶：</strong>你可以设计一个时间复杂度为 <code>O(n)</code> 的解决方案吗？</p>
</div>
</div>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/shortest-unsorted-continuous-subarray/description/)  -  [LeetCode-CN](https://leetcode.cn/problems/shortest-unsorted-continuous-subarray/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| typescript  | 100 ms | 46.4 MB | 2023/08/12 19:38 |

```typescript

function findUnsortedSubarray(nums: number[]): number {
  if (isSorted(nums)) {
    return 0;
  }

  const sortedArr = [...nums].sort((a, b) => a - b);

  let start = -1, end = -1;

  for (let i = 0; i < nums.length; i++) {
    if (nums[i] !== sortedArr[i]) {
      start = i;
      break;
    }
  }

  for (let j = nums.length - 1; j > 0; j--) {
    if (nums[j] !== sortedArr[j]) {
      end = j;
      break;
    }
  }

  return end - start + 1;
};

const isSorted = (nums: number[]) => {
  if (nums.length <= 1) {
    return true;
  }
  for (let i = 1; i < nums.length; i++) {
    if (nums[i] < nums[i - 1]) {
      return false;
    }
  }

  return true;
}

```
## My Notes - 我的笔记


简单排序之后比较即可。

```typescript
function findUnsortedSubarray(nums: number[]): number {
  if (isSorted(nums)) {
    return 0;
  }

  const sortedArr = [...nums].sort((a, b) => a - b);

  let start = -1, end = -1;

  for (let i = 0; i < nums.length; i++) {
    if (nums[i] !== sortedArr[i]) {
      start = i;
      break;
    }
  }

  for (let j = nums.length - 1; j > 0; j--) {
    if (nums[j] !== sortedArr[j]) {
      end = j;
      break;
    }
  }

  return end - start + 1;
};

const isSorted = (nums: number[]) => {
  if (nums.length <= 1) {
    return true;
  }
  for (let i = 1; i < nums.length; i++) {
    if (nums[i] < nums[i - 1]) {
      return false;
    }
  }

  return true;
}
```

