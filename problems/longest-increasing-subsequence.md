
# 300. Longest Increasing Subsequence - 最长递增子序列

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Array-数组-blue.svg">   <img src="https://img.shields.io/badge/Binary Search-二分查找-blue.svg">   <img src="https://img.shields.io/badge/Dynamic Programming-动态规划-blue.svg">  


## Description - 题目描述

### EN:
<p>Given an integer array <code>nums</code>, return <em>the length of the longest <strong>strictly increasing </strong></em><span data-keyword="subsequence-array"><em><strong>subsequence</strong></em></span>.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input:</strong> nums = [10,9,2,5,3,7,101,18]
<strong>Output:</strong> 4
<strong>Explanation:</strong> The longest increasing subsequence is [2,3,7,101], therefore the length is 4.
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre>
<strong>Input:</strong> nums = [0,1,0,3,2,3]
<strong>Output:</strong> 4
</pre>

<p><strong class="example">Example 3:</strong></p>

<pre>
<strong>Input:</strong> nums = [7,7,7,7,7,7,7]
<strong>Output:</strong> 1
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= nums.length &lt;= 2500</code></li>
	<li><code>-10<sup>4</sup> &lt;= nums[i] &lt;= 10<sup>4</sup></code></li>
</ul>

<p>&nbsp;</p>
<p><b>Follow up:</b>&nbsp;Can you come up with an algorithm that runs in&nbsp;<code>O(n log(n))</code> time complexity?</p>


### ZH-CN:
<p>给你一个整数数组 <code>nums</code> ，找到其中最长严格递增子序列的长度。</p>

<p><strong>子序列&nbsp;</strong>是由数组派生而来的序列，删除（或不删除）数组中的元素而不改变其余元素的顺序。例如，<code>[3,6,2,7]</code> 是数组 <code>[0,3,1,6,2,2,7]</code> 的子序列。</p>
&nbsp;

<p><strong>示例 1：</strong></p>

<pre>
<strong>输入：</strong>nums = [10,9,2,5,3,7,101,18]
<strong>输出：</strong>4
<strong>解释：</strong>最长递增子序列是 [2,3,7,101]，因此长度为 4 。
</pre>

<p><strong>示例 2：</strong></p>

<pre>
<strong>输入：</strong>nums = [0,1,0,3,2,3]
<strong>输出：</strong>4
</pre>

<p><strong>示例 3：</strong></p>

<pre>
<strong>输入：</strong>nums = [7,7,7,7,7,7,7]
<strong>输出：</strong>1
</pre>

<p>&nbsp;</p>

<p><strong>提示：</strong></p>

<ul>
	<li><code>1 &lt;= nums.length &lt;= 2500</code></li>
	<li><code>-10<sup>4</sup> &lt;= nums[i] &lt;= 10<sup>4</sup></code></li>
</ul>

<p>&nbsp;</p>

<p><b>进阶：</b></p>

<ul>
	<li>你能将算法的时间复杂度降低到&nbsp;<code>O(n log(n))</code> 吗?</li>
</ul>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/longest-increasing-subsequence/description/)  -  [LeetCode-CN](https://leetcode.cn/problems/longest-increasing-subsequence/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| typescript  | 180 ms | 43.9 MB | 2023/03/26 17:16 |

```typescript

function lengthOfLIS(nums: number[]): number {
  if (nums.length === 1) {
    return 1;
  }

  const dp: number[] = new Array(nums.length).fill(1);

  dp[0] = 1;

  for (let i = 1; i < nums.length; ++i) {
    for (let j = 0; j < i; ++j) {
      if (nums[i] > nums[j]) {
        dp[i] = Math.max(dp[i], dp[j] + 1);
      }
    }
  }

  return Math.max(...dp);

};

```
## My Notes - 我的笔记


# 动态规划
刚开始想的状态转移方程是$dp[i] = nums[i] > nums[i-1] ? dp[i - 1] + 1: dp[i]$
但这样就不符合 以`i`为结尾了。
因此应该为： ${dp[i] = max\{dp[j] + 1\}}, j \in [0, i]$

```typescript
function lengthOfLIS(nums: number[]): number {
  if (nums.length === 1) {
    return 1;
  }

  const dp: number[] = new Array(nums.length).fill(1);

  dp[0] = 1;

  for (let i = 1; i < nums.length; ++i) {
    for (let j = 0; j < i; ++j) {
      if (nums[i] > nums[j]) {
        dp[i] = Math.max(dp[i], dp[j] + 1);
      }
    }
  }

  return Math.max(...dp);

};
```

# 贪心+二分
思路：维护一个单调递增的子序列。
注意到这个子序列单增，可以用二分查找。
需要子序列尽可能长，使用贪心的思想，即加入子序列的尾部数字尽可能小。

因此，算法是：
1. 遍历 nums;
2. 当 `nums[i]` 大于子序列 `d`的最后一个数，插入；
3. 当 `nums[i]` 大于子序列 `d`的最后一个数，在 `d` 中二分查找比`nums[i]` 小的第一个数`d[k]`; 如果 `d[k+1] > nums[i]` ，则令`d[k+1] = nums[i]`，确保 `d `中的数尽可能小。

