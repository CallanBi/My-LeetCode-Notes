
# 560. Subarray Sum Equals K - 和为 K 的子数组

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Array-数组-blue.svg">   <img src="https://img.shields.io/badge/Hash Table-哈希表-blue.svg">   <img src="https://img.shields.io/badge/Prefix Sum-前缀和-blue.svg">  


## Description - 题目描述

### EN:
<p>Given an array of integers <code>nums</code> and an integer <code>k</code>, return <em>the total number of subarrays whose sum equals to</em> <code>k</code>.</p>

<p>A subarray is a contiguous <strong>non-empty</strong> sequence of elements within an array.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>
<pre><strong>Input:</strong> nums = [1,1,1], k = 2
<strong>Output:</strong> 2
</pre><p><strong class="example">Example 2:</strong></p>
<pre><strong>Input:</strong> nums = [1,2,3], k = 3
<strong>Output:</strong> 2
</pre>
<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= nums.length &lt;= 2 * 10<sup>4</sup></code></li>
	<li><code>-1000 &lt;= nums[i] &lt;= 1000</code></li>
	<li><code>-10<sup>7</sup> &lt;= k &lt;= 10<sup>7</sup></code></li>
</ul>


### ZH-CN:
<p>给你一个整数数组 <code>nums</code> 和一个整数&nbsp;<code>k</code> ，请你统计并返回 <em>该数组中和为&nbsp;<code>k</code><strong>&nbsp;</strong>的连续子数组的个数&nbsp;</em>。</p>

<p>&nbsp;</p>

<p><strong>示例 1：</strong></p>

<pre>
<strong>输入：</strong>nums = [1,1,1], k = 2
<strong>输出：</strong>2
</pre>

<p><strong>示例 2：</strong></p>

<pre>
<strong>输入：</strong>nums = [1,2,3], k = 3
<strong>输出：</strong>2
</pre>

<p>&nbsp;</p>

<p><strong>提示：</strong></p>

<ul>
	<li><code>1 &lt;= nums.length &lt;= 2 * 10<sup>4</sup></code></li>
	<li><code>-1000 &lt;= nums[i] &lt;= 1000</code></li>
	<li><code>-10<sup>7</sup> &lt;= k &lt;= 10<sup>7</sup></code></li>
</ul>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/subarray-sum-equals-k/description/)  -  [LeetCode-CN](https://leetcode.cn/problems/subarray-sum-equals-k/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| typescript  | 100 ms | 51.2 MB | 2023/08/12 19:22 |

```typescript

function subarraySum(nums: number[], k: number): number {
  const preSum: number[] = [0];

  const preSumHash = new Map<number, number>();

  preSumHash.set(0, 1);

  let count = 0;

  for (let i = 0; i < nums.length; i++) {
    preSum[i + 1] = preSum[i] + nums[i];

    const prev = preSumHash.get(preSum[i + 1] - k);

    if (prev !== undefined) {
      count += prev;
    }

    const cur = preSumHash.get(preSum[i + 1]);

    if (cur !== undefined) {
      preSumHash.set(preSum[i + 1], cur + 1)
    } else {
      preSumHash.set(preSum[i + 1], 1);
    }
  }

  return count;
};

```
## My Notes - 我的笔记


# 哈希表+前缀和
思路与官方题解一致:  时间复杂度 $O(n)$

但要注意：哈希表需要存的是能满足 $preSum[i - 1] == preSum[j] - k$ 的 $i$ 的个数，而不是前缀和数组下标（因为满足 $preSum[i - 1] == preSum[j] - k$ 的 $i$ 可能有多个）。

如果存下标，代码需要变成这样：

```typescript
function subarraySum(nums: number[], k: number): number {
  const preSum: number[] = [0];

  const preSumHash = new Map<number, number[]>();

  preSumHash.set(0, [0]);

  let count = 0;

  for (let i = 0; i < nums.length; i++) {
    preSum[i + 1] = preSum[i] + nums[i];
    const prev = preSumHash.get(preSum[i + 1] - k);

    if (prev !== undefined) {
      count += prev.length;
    }

    const cur = preSumHash.get(preSum[i + 1]);

    if (cur !== undefined) {
      cur.push(i + 1);
    } else {
      preSumHash.set(preSum[i + 1], [i + 1]);
    }
  }

  return count;
};
```

实际上存个数，代码更简单：

```typescript
function subarraySum(nums: number[], k: number): number {
  const preSum: number[] = [0];

  const preSumHash = new Map<number, number>();

  preSumHash.set(0, 1);

  let count = 0;

  for (let i = 0; i < nums.length; i++) {
    preSum[i + 1] = preSum[i] + nums[i];

    const prev = preSumHash.get(preSum[i + 1] - k);

    if (prev !== undefined) {
      count += prev;
    }

    const cur = preSumHash.get(preSum[i + 1]);

    if (cur !== undefined) {
      preSumHash.set(preSum[i + 1], cur + 1)
    } else {
      preSumHash.set(preSum[i + 1], 1);
    }
  }

  return count;
};
```



