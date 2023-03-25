
# 283. Move Zeroes - 移动零

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Array-数组-blue.svg">   <img src="https://img.shields.io/badge/Two Pointers-双指针-blue.svg">  


## Description - 题目描述

### EN:
<p>Given an integer array <code>nums</code>, move all <code>0</code>&#39;s to the end of it while maintaining the relative order of the non-zero elements.</p>

<p><strong>Note</strong> that you must do this in-place without making a copy of the array.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>
<pre><strong>Input:</strong> nums = [0,1,0,3,12]
<strong>Output:</strong> [1,3,12,0,0]
</pre><p><strong class="example">Example 2:</strong></p>
<pre><strong>Input:</strong> nums = [0]
<strong>Output:</strong> [0]
</pre>
<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= nums.length &lt;= 10<sup>4</sup></code></li>
	<li><code>-2<sup>31</sup> &lt;= nums[i] &lt;= 2<sup>31</sup> - 1</code></li>
</ul>

<p>&nbsp;</p>
<strong>Follow up:</strong> Could you minimize the total number of operations done?

### ZH-CN:
<p>给定一个数组 <code>nums</code>，编写一个函数将所有 <code>0</code> 移动到数组的末尾，同时保持非零元素的相对顺序。</p>

<p><strong>请注意</strong>&nbsp;，必须在不复制数组的情况下原地对数组进行操作。</p>

<p>&nbsp;</p>

<p><strong>示例 1:</strong></p>

<pre>
<strong>输入:</strong> nums = <code>[0,1,0,3,12]</code>
<strong>输出:</strong> <code>[1,3,12,0,0]</code>
</pre>

<p><strong>示例 2:</strong></p>

<pre>
<strong>输入:</strong> nums = <code>[0]</code>
<strong>输出:</strong> <code>[0]</code></pre>

<p>&nbsp;</p>

<p><strong>提示</strong>:</p>
<meta charset="UTF-8" />

<ul>
	<li><code>1 &lt;= nums.length &lt;= 10<sup>4</sup></code></li>
	<li><code>-2<sup>31</sup>&nbsp;&lt;= nums[i] &lt;= 2<sup>31</sup>&nbsp;- 1</code></li>
</ul>

<p>&nbsp;</p>

<p><b>进阶：</b>你能尽量减少完成的操作次数吗？</p>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/move-zeroes/description/)  -  [LeetCode-CN](https://leetcode.cn/problems/move-zeroes/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| typescript  | 88 ms | 46.5 MB | 2023/03/25 21:27 |

```typescript

/**
 Do not return anything, modify nums in-place instead.
 */
function moveZeroes(nums: number[]): void {
  let endWithZero = nums.findIndex(i => i === 0);

  if (endWithZero === -1) {
    return;
  }

  for (let i = endWithZero + 1; i < nums.length; i++) {
    if (nums[i] !== 0) {
      nums[endWithZero] = nums[i];
      endWithZero += 1;
    }
  }


  for (; endWithZero < nums.length; endWithZero++) {
    nums[endWithZero] = 0;
  }
};

```
## My Notes - 我的笔记


# 两个指针一前一后
思路：一前一后两个指针，前指针先找到第一个0的位置，后指针从前指针+1开始遍历；
遇到0不处理，遇到非0则将后指针所在值赋给前指针所在值，并前指针+1;
后指针遍历完数组，将前指针后的数字全赋0即可。
```typescript
/**
 Do not return anything, modify nums in-place instead.
 */
function moveZeroes(nums: number[]): void {
  let endWithZero = nums.findIndex(i => i === 0);

  if (endWithZero === -1) {
    return;
  }

  for (let i = endWithZero + 1; i < nums.length; i++) {
    if (nums[i] !== 0) {
      nums[endWithZero] = nums[i];
      endWithZero += 1;
    }
  }


  for (; endWithZero < nums.length; endWithZero++) {
    nums[endWithZero] = 0;
  }
};
```

