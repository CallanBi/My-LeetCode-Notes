
# 198. House Robber - 打家劫舍

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Array-数组-blue.svg">   <img src="https://img.shields.io/badge/Dynamic Programming-动态规划-blue.svg">  


## Description - 题目描述

### EN:
<p>You are a professional robber planning to rob houses along a street. Each house has a certain amount of money stashed, the only constraint stopping you from robbing each of them is that adjacent houses have security systems connected and <b>it will automatically contact the police if two adjacent houses were broken into on the same night</b>.</p>

<p>Given an integer array <code>nums</code> representing the amount of money of each house, return <em>the maximum amount of money you can rob tonight <b>without alerting the police</b></em>.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input:</strong> nums = [1,2,3,1]
<strong>Output:</strong> 4
<strong>Explanation:</strong> Rob house 1 (money = 1) and then rob house 3 (money = 3).
Total amount you can rob = 1 + 3 = 4.
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre>
<strong>Input:</strong> nums = [2,7,9,3,1]
<strong>Output:</strong> 12
<strong>Explanation:</strong> Rob house 1 (money = 2), rob house 3 (money = 9) and rob house 5 (money = 1).
Total amount you can rob = 2 + 9 + 1 = 12.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= nums.length &lt;= 100</code></li>
	<li><code>0 &lt;= nums[i] &lt;= 400</code></li>
</ul>


### ZH-CN:
<p>你是一个专业的小偷，计划偷窃沿街的房屋。每间房内都藏有一定的现金，影响你偷窃的唯一制约因素就是相邻的房屋装有相互连通的防盗系统，<strong>如果两间相邻的房屋在同一晚上被小偷闯入，系统会自动报警</strong>。</p>

<p>给定一个代表每个房屋存放金额的非负整数数组，计算你<strong> 不触动警报装置的情况下 </strong>，一夜之内能够偷窃到的最高金额。</p>

<p> </p>

<p><strong>示例 1：</strong></p>

<pre>
<strong>输入：</strong>[1,2,3,1]
<strong>输出：</strong>4
<strong>解释：</strong>偷窃 1 号房屋 (金额 = 1) ，然后偷窃 3 号房屋 (金额 = 3)。
     偷窃到的最高金额 = 1 + 3 = 4 。</pre>

<p><strong>示例 2：</strong></p>

<pre>
<strong>输入：</strong>[2,7,9,3,1]
<strong>输出：</strong>12
<strong>解释：</strong>偷窃 1 号房屋 (金额 = 2), 偷窃 3 号房屋 (金额 = 9)，接着偷窃 5 号房屋 (金额 = 1)。
     偷窃到的最高金额 = 2 + 9 + 1 = 12 。
</pre>

<p> </p>

<p><strong>提示：</strong></p>

<ul>
	<li><code>1 <= nums.length <= 100</code></li>
	<li><code>0 <= nums[i] <= 400</code></li>
</ul>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/house-robber/description/)  -  [LeetCode-CN](https://leetcode.cn/problems/house-robber/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| typescript  | 56 ms | 42.2 MB | 2023/03/04 23:49 |

```typescript

function rob(nums: number[]): number {
  if (nums.length === 1) {
    return nums[0];
  }

  const dp: number[] = new Array(nums.length).fill(0);

  dp[0] = nums[0];
  dp[1] = Math.max(nums[0], nums[1]);

  for (let i = 2; i < nums.length; i++) {
    dp[i] = Math.max(nums[i] + dp[i-2], dp[i - 1]);
  }

  return dp[dp.length - 1];
};

```
## My Notes - 我的笔记


最初的思路：用 dp。

用 dp[i] 表示如果偷第`i` 间房，可以偷的最大金额。

本来想的是$nums[i] + dp[i - 2]$，后来发现 `[2,1,1,2]` 这个用例，如果这样的话输出是3，应该选第1个元素和最后一个元素。
所以改了下应该是$nums[i] + max\{dp[0], dp[1], ..., dp[i - 2]\}$。

```
function rob(nums: number[]): number {
  if (nums.length === 1) {
    return nums[0];
  }

  const dp: number[] = new Array(nums.length).fill(0);

  for (let i = 0; i < nums.length; i++) {
    if (i - 2 < 0) {
      dp[i] = nums[i];
    } else {
      dp[i] = nums[i] + Math.max(...dp.slice(0, i - 1));
    }
  }

  return Math.max(...dp);
};
```

看了官方题解，好像确实不用 `Math.max(...dp.slice(0, i - 1))`，只需要比较 `dp[i-1]` 的值就行。

而且官方题解的 dp 直接就是最大金额。所以它是这样实现的：
```typescript
function rob(nums: number[]): number {
  if (nums.length === 1) {
    return nums[0];
  }

  const dp: number[] = new Array(nums.length).fill(0);

  dp[0] = nums[0];
  dp[1] = Math.max(nums[0], nums[1]);

  for (let i = 2; i < nums.length; i++) {
    dp[i] = Math.max(nums[i] + dp[i-2], dp[i - 1]);
  }

  return dp[dp.length - 1];
};
```

这样一看少了一次遍历，更快了。


