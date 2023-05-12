
# 416. Partition Equal Subset Sum - 分割等和子集

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Array-数组-blue.svg">   <img src="https://img.shields.io/badge/Dynamic Programming-动态规划-blue.svg">  


## Description - 题目描述

### EN:
<p>Given an integer array <code>nums</code>, return <code>true</code> <em>if you can partition the array into two subsets such that the sum of the elements in both subsets is equal or </em><code>false</code><em> otherwise</em>.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input:</strong> nums = [1,5,11,5]
<strong>Output:</strong> true
<strong>Explanation:</strong> The array can be partitioned as [1, 5, 5] and [11].
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre>
<strong>Input:</strong> nums = [1,2,3,5]
<strong>Output:</strong> false
<strong>Explanation:</strong> The array cannot be partitioned into equal sum subsets.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= nums.length &lt;= 200</code></li>
	<li><code>1 &lt;= nums[i] &lt;= 100</code></li>
</ul>


### ZH-CN:
<p>给你一个 <strong>只包含正整数 </strong>的 <strong>非空 </strong>数组 <code>nums</code> 。请你判断是否可以将这个数组分割成两个子集，使得两个子集的元素和相等。</p>

<p> </p>

<p><strong>示例 1：</strong></p>

<pre>
<strong>输入：</strong>nums = [1,5,11,5]
<strong>输出：</strong>true
<strong>解释：</strong>数组可以分割成 [1, 5, 5] 和 [11] 。</pre>

<p><strong>示例 2：</strong></p>

<pre>
<strong>输入：</strong>nums = [1,2,3,5]
<strong>输出：</strong>false
<strong>解释：</strong>数组不能分割成两个元素和相等的子集。
</pre>

<p> </p>

<p><strong>提示：</strong></p>

<ul>
	<li><code>1 <= nums.length <= 200</code></li>
	<li><code>1 <= nums[i] <= 100</code></li>
</ul>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/partition-equal-subset-sum/description/)  -  [LeetCode-CN](https://leetcode.cn/problems/partition-equal-subset-sum/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| typescript  | 112 ms | 43.9 MB | 2023/05/12 13:34 |

```typescript

function canPartition(nums: number[]): boolean {
  if (nums.length < 2) {
    return false;
  }

  const sum = nums.reduce((acc, cur, idx, arr) => {
    return acc + cur;
  }, 0);

  if (sum % 2 !== 0) {
    return false;
  }

  if (nums.findIndex(e => e > sum / 2) !== -1) {
    return false;
  }

  const dp = new Array(sum / 2 + 1).fill(false);

  // 若从[0, i]索引的集合中不选取任何数，则可以使得和为0，因此边界条件为 dp[0] = true
  dp[0] = true;

  for (let i = 0; i < nums.length; i++) {
    for (let j = sum / 2; j >= 0; j--) {
      if (nums[i] <= j) {
        dp[j] = dp[j] || dp[j - nums[i]];
      }
    }
  }


  return dp[sum / 2];
};

```
## My Notes - 我的笔记


No notes

