
# 448. Find All Numbers Disappeared in an Array - 找到所有数组中消失的数字

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Array-数组-blue.svg">   <img src="https://img.shields.io/badge/Hash Table-哈希表-blue.svg">  


## Description - 题目描述

### EN:
<p>Given an array <code>nums</code> of <code>n</code> integers where <code>nums[i]</code> is in the range <code>[1, n]</code>, return <em>an array of all the integers in the range</em> <code>[1, n]</code> <em>that do not appear in</em> <code>nums</code>.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>
<pre><strong>Input:</strong> nums = [4,3,2,7,8,2,3,1]
<strong>Output:</strong> [5,6]
</pre><p><strong class="example">Example 2:</strong></p>
<pre><strong>Input:</strong> nums = [1,1]
<strong>Output:</strong> [2]
</pre>
<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>n == nums.length</code></li>
	<li><code>1 &lt;= n &lt;= 10<sup>5</sup></code></li>
	<li><code>1 &lt;= nums[i] &lt;= n</code></li>
</ul>

<p>&nbsp;</p>
<p><strong>Follow up:</strong> Could you do it without extra space and in <code>O(n)</code> runtime? You may assume the returned list does not count as extra space.</p>


### ZH-CN:
<p>给你一个含 <code>n</code> 个整数的数组 <code>nums</code> ，其中 <code>nums[i]</code> 在区间 <code>[1, n]</code> 内。请你找出所有在 <code>[1, n]</code> 范围内但没有出现在 <code>nums</code> 中的数字，并以数组的形式返回结果。</p>

<p> </p>

<p><strong>示例 1：</strong></p>

<pre>
<strong>输入：</strong>nums = [4,3,2,7,8,2,3,1]
<strong>输出：</strong>[5,6]
</pre>

<p><strong>示例 2：</strong></p>

<pre>
<strong>输入：</strong>nums = [1,1]
<strong>输出：</strong>[2]
</pre>

<p> </p>

<p><strong>提示：</strong></p>

<ul>
	<li><code>n == nums.length</code></li>
	<li><code>1 <= n <= 10<sup>5</sup></code></li>
	<li><code>1 <= nums[i] <= n</code></li>
</ul>

<p><strong>进阶：</strong>你能在不使用额外空间且时间复杂度为<em> </em><code>O(n)</code><em> </em>的情况下解决这个问题吗? 你可以假定返回的数组不算在额外空间内。</p>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/find-all-numbers-disappeared-in-an-array/description/)  -  [LeetCode-CN](https://leetcode.cn/problems/find-all-numbers-disappeared-in-an-array/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| typescript  | 160 ms | 59.8 MB | 2023/07/23 12:50 |

```typescript

function findDisappearedNumbers(nums: number[]): number[] {
  const n = nums.length;
  let count = 0;

  for (let i = 0; i < n; i++) {
    nums[n + nums[i] - 1] = 1;
  }

  for (let i = n; i < 2 * n; i++) {
    if (nums[i] !== 1) {
      nums[n + count] = i - n + 1;
      count++;
    }
  }

  return nums.slice(n, n + count);
};

```
## My Notes - 我的笔记


不同于「找到数组中重复数字」这道题是用赋值到相应位置做，「找到所有数组消失的数字」不能这样做。

解法：利用长度为 $n$ 的哈希表，直接在原数组中原地存储，若数字存在则置为1。最后答案仍然存储在原数组中，截取答案返回即可。

```typescript
function findDisappearedNumbers(nums: number[]): number[] {
  const n = nums.length;
  let count = 0;

  for (let i = 0; i < n; i++) {
    nums[n + nums[i] - 1] = 1;
  }

  for (let i = n; i < 2 * n; i++) {
    if (nums[i] !== 1) {
      nums[n + count] = i - n + 1;
      count++;
    }
  }

  return nums.slice(n, n + count);
};
```

