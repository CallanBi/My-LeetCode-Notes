
# 75. Sort Colors - 颜色分类

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Array-数组-blue.svg">   <img src="https://img.shields.io/badge/Two Pointers-双指针-blue.svg">   <img src="https://img.shields.io/badge/Sorting-排序-blue.svg">  


## Description - 题目描述

### EN:
<p>Given an array <code>nums</code> with <code>n</code> objects colored red, white, or blue, sort them <strong><a href="https://en.wikipedia.org/wiki/In-place_algorithm" target="_blank">in-place</a> </strong>so that objects of the same color are adjacent, with the colors in the order red, white, and blue.</p>

<p>We will use the integers <code>0</code>, <code>1</code>, and <code>2</code> to represent the color red, white, and blue, respectively.</p>

<p>You must solve this problem without using the library&#39;s sort function.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input:</strong> nums = [2,0,2,1,1,0]
<strong>Output:</strong> [0,0,1,1,2,2]
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre>
<strong>Input:</strong> nums = [2,0,1]
<strong>Output:</strong> [0,1,2]
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>n == nums.length</code></li>
	<li><code>1 &lt;= n &lt;= 300</code></li>
	<li><code>nums[i]</code> is either <code>0</code>, <code>1</code>, or <code>2</code>.</li>
</ul>

<p>&nbsp;</p>
<p><strong>Follow up:</strong>&nbsp;Could you come up with a one-pass algorithm using only&nbsp;constant extra space?</p>


### ZH-CN:
<p>给定一个包含红色、白色和蓝色、共&nbsp;<code>n</code><em> </em>个元素的数组<meta charset="UTF-8" />&nbsp;<code>nums</code>&nbsp;，<strong><a href="https://baike.baidu.com/item/%E5%8E%9F%E5%9C%B0%E7%AE%97%E6%B3%95" target="_blank">原地</a></strong>对它们进行排序，使得相同颜色的元素相邻，并按照红色、白色、蓝色顺序排列。</p>

<p>我们使用整数 <code>0</code>、&nbsp;<code>1</code> 和 <code>2</code> 分别表示红色、白色和蓝色。</p>

<ul>
</ul>

<p>必须在不使用库内置的 sort 函数的情况下解决这个问题。</p>

<p>&nbsp;</p>

<p><strong>示例 1：</strong></p>

<pre>
<strong>输入：</strong>nums = [2,0,2,1,1,0]
<strong>输出：</strong>[0,0,1,1,2,2]
</pre>

<p><strong>示例 2：</strong></p>

<pre>
<strong>输入：</strong>nums = [2,0,1]
<strong>输出：</strong>[0,1,2]
</pre>

<p>&nbsp;</p>

<p><strong>提示：</strong></p>

<ul>
	<li><code>n == nums.length</code></li>
	<li><code>1 &lt;= n &lt;= 300</code></li>
	<li><code>nums[i]</code> 为 <code>0</code>、<code>1</code> 或 <code>2</code></li>
</ul>

<p>&nbsp;</p>

<p><strong>进阶：</strong></p>

<ul>
	<li>你能想出一个仅使用常数空间的一趟扫描算法吗？</li>
</ul>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/sort-colors/description/)  -  [LeetCode-CN](https://leetcode.cn/problems/sort-colors/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| typescript  | 64 ms | 43.4 MB | 2022/05/30 14:57 |

```typescript

/**
 Do not return anything, modify nums in-place instead.
 */
function sortColors(nums: number[]): void {
  if (nums.length === 1) {
    return;
  }

  let ptr0 = 0, ptr2 = nums.length - 1;

  for (let i = 0; i <= ptr2; i++) {
    for (; i <= ptr2 && nums[i] === 2; ptr2--) {
      [nums[ptr2], nums[i]] = [nums[i], nums[ptr2]];
    }
    if (nums[i] === 0) {
      [nums[ptr0], nums[i]] = [nums[i], nums[ptr0]];
      ptr0++;
    }
  }
};

```
## My Notes - 我的笔记


参考[官方题解](https://leetcode.cn/problems/sort-colors/solution/yan-se-fen-lei-by-leetcode-solution/) 中双指针的第二种方法。
```typescript
/**
 Do not return anything, modify nums in-place instead.
 */
function sortColors(nums: number[]): void {
  if (nums.length === 1) {
    return;
  }

  let ptr0 = 0, ptr2 = nums.length - 1;

  for (let i = 0; i <= ptr2; i++) {
    // 注意这个 for 循环 和 if (nums[i] === 0) 语句的顺序
    for (; i <= ptr2 && nums[i] === 2; ptr2--) {
      [nums[ptr2], nums[i]] = [nums[i], nums[ptr2]];
    }
    if (nums[i] === 0) {
      [nums[ptr0], nums[i]] = [nums[i], nums[ptr0]];
      ptr0++;
    }
  }
};
```

