
# 128. Longest Consecutive Sequence - 最长连续序列

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Union Find-并查集-blue.svg">   <img src="https://img.shields.io/badge/Array-数组-blue.svg">   <img src="https://img.shields.io/badge/Hash Table-哈希表-blue.svg">  


## Description - 题目描述

### EN:
<p>Given an unsorted array of integers <code>nums</code>, return <em>the length of the longest consecutive elements sequence.</em></p>

<p>You must write an algorithm that runs in&nbsp;<code>O(n)</code>&nbsp;time.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input:</strong> nums = [100,4,200,1,3,2]
<strong>Output:</strong> 4
<strong>Explanation:</strong> The longest consecutive elements sequence is <code>[1, 2, 3, 4]</code>. Therefore its length is 4.
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre>
<strong>Input:</strong> nums = [0,3,7,2,5,8,4,6,0,1]
<strong>Output:</strong> 9
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>0 &lt;= nums.length &lt;= 10<sup>5</sup></code></li>
	<li><code>-10<sup>9</sup> &lt;= nums[i] &lt;= 10<sup>9</sup></code></li>
</ul>


### ZH-CN:
<p>给定一个未排序的整数数组 <code>nums</code> ，找出数字连续的最长序列（不要求序列元素在原数组中连续）的长度。</p>

<p>请你设计并实现时间复杂度为 <code>O(n)</code><em> </em>的算法解决此问题。</p>

<p> </p>

<p><strong>示例 1：</strong></p>

<pre>
<strong>输入：</strong>nums = [100,4,200,1,3,2]
<strong>输出：</strong>4
<strong>解释：</strong>最长数字连续序列是 <code>[1, 2, 3, 4]。它的长度为 4。</code></pre>

<p><strong>示例 2：</strong></p>

<pre>
<strong>输入：</strong>nums = [0,3,7,2,5,8,4,6,0,1]
<strong>输出：</strong>9
</pre>

<p> </p>

<p><strong>提示：</strong></p>

<ul>
	<li><code>0 <= nums.length <= 10<sup>5</sup></code></li>
	<li><code>-10<sup>9</sup> <= nums[i] <= 10<sup>9</sup></code></li>
</ul>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/longest-consecutive-sequence/description/)  -  [LeetCode-CN](https://leetcode.cn/problems/longest-consecutive-sequence/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| typescript  | 100 ms | 56.6 MB | 2022/09/03 19:05 |

```typescript

function longestConsecutive(nums: number[]): number {
  const s = new Set<number>(nums);

  let longestLength = 0;

  for (let i of s) {
    if (s.has(i - 1)) {
      continue;
    }

    let curLength = 1;

    let j = i + 1;

    while (s.has(j)) {
      curLength += 1;
      j += 1;
    }

    longestLength = Math.max(longestLength, curLength);
  }

  return longestLength;
};

```
## My Notes - 我的笔记


参考了官方题解的解法：
```typescript
function longestConsecutive(nums: number[]): number {
  const s = new Set<number>(nums);

  let longestLength = 0;

  for (let i of s) {
    if (s.has(i - 1)) {
      continue;
    }

    let curLength = 1;

    let j = i + 1;

    while (s.has(j)) {
      curLength += 1;
      j += 1;
    }

    longestLength = Math.max(longestLength, curLength);
  }

  return longestLength;
};
```

注意```s.has(j)``` 不要写成```s.has[j]```。

