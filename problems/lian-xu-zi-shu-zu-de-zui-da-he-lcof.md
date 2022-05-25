
# 剑指 Offer 42. 连续子数组的最大和  LCOF - 连续子数组的最大和

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Array-数组-blue.svg">   <img src="https://img.shields.io/badge/Divide and Conquer-分治-blue.svg">   <img src="https://img.shields.io/badge/Dynamic Programming-动态规划-blue.svg">  


## Description - 题目描述

### EN:
English description is not available for the problem. Please switch to Chinese.

### ZH-CN:
<p>输入一个整型数组，数组中的一个或连续多个整数组成一个子数组。求所有子数组的和的最大值。</p>

<p>要求时间复杂度为O(n)。</p>

<p>&nbsp;</p>

<p><strong>示例1:</strong></p>

<pre><strong>输入:</strong> nums = [-2,1,-3,4,-1,2,1,-5,4]
<strong>输出:</strong> 6
<strong>解释:</strong>&nbsp;连续子数组&nbsp;[4,-1,2,1] 的和最大，为&nbsp;6。</pre>

<p>&nbsp;</p>

<p><strong>提示：</strong></p>

<ul>
	<li><code>1 &lt;=&nbsp;arr.length &lt;= 10^5</code></li>
	<li><code>-100 &lt;= arr[i] &lt;= 100</code></li>
</ul>

<p>注意：本题与主站 53 题相同：<a href="https://leetcode-cn.com/problems/maximum-subarray/">https://leetcode-cn.com/problems/maximum-subarray/</a></p>

<p>&nbsp;</p>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/lian-xu-zi-shu-zu-de-zui-da-he-lcof/description/)  -  [LeetCode-CN](https://leetcode.cn/problems/lian-xu-zi-shu-zu-de-zui-da-he-lcof/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| typescript  | 72 ms | 42.4 MB | 2021/12/14 19:32 |

```typescript

function maxSubArray(nums: number[]): number {
  let pre = nums[0];
  let curMax = 0, max = nums[0];
  const len = nums.length;
  for (let i = 1; i < len; i++) {
    if (pre <= 0) {
      curMax = nums[i];
    } else {
      curMax = pre + nums[i];
    }
    pre = curMax;
    max = Math.max(max, curMax);
  }
  return max;
};

```
## My Notes - 我的笔记


本题与主站 53 题相同：<https://leetcode-cn.com/problems/maximum-subarray/>

# 方法一：动态规划

知道是用 dp，但如何跳出思维误区？

动态规划题的答案并不仅仅只有 `dp[n]`。也可以是`max{dp[]}`等，即外面套一个函数。

比如这道题，如果设 f(n)为截取索引为 0 - n 的数组切片中的所有连续子数组的和的最大值，将会非常麻烦，找不到规律。

但如果设 f(n)为索引为 0 - n 的数组切片中，包括 `nums[n]`在内的连续子数组的和的最大值，则规律就十分明显了。

如果`f(n-1) > 0`， 即包括之前一个索引所构成的连续子数组和大于0，则不管 `nums[n]`是否大于0（因为必须要包括`nums[n]`），直接将 `nums[n-1]` 拼接到之前的子数组即可。此时该拼接的数组必定是连续的(因为 `f(n-1)` 也包括了 `nums[n-1]`)。即 `f(n) = f(n-1) + nums[n]`。

如果`f(n-1) <= 0`， 即包括之前一个索引所构成的连续子数组和小于等于0，则抛弃之前的子数组，直接用 `nums[n]` 构成一个子数组。即 `f(n) = nums[n]`。

当 dp 求完之后，直接 `max{dp}`就可以得到所有连续子数组的和的最大值。

时间复杂度为 O(n)，空间复杂度为 O(n)。

```typescript
function maxSubArray(nums: number[]): number {
  const dp: number[] = [];
  dp[0] = nums[0];
  const len = nums.length;
  for (let i = 1; i < len; i++) {
    if (dp[i-1] <= 0) {
      dp[i] = nums[i];
    } else {
      dp[i] = dp[i-1] + nums[i];
    }
  }
  return Math.max(...dp);
};
```

下面这段是参考了官方题解，

> 考虑到 f(i) 只和 f(i-1) 相关，于是我们可以只用一个变量 pre 来维护对于当前 f(i) 的 f(i-1) 的值是多少，从而让空间复杂度降低到 O(1）。

优化空间复杂度的代码：

```typescript
function maxSubArray(nums: number[]): number {
  let pre = nums[0];
  let curMax = 0, max = nums[0];
  const len = nums.length;
  for (let i = 1; i < len; i++) {
    if (pre <= 0) {
      curMax = nums[i];
    } else {
      curMax = pre + nums[i];
    }
    pre = curMax;
    max = Math.max(max, curMax);
  }
  return max;
};
```


