
# 238. Product of Array Except Self - 除自身以外数组的乘积

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Array-数组-blue.svg">   <img src="https://img.shields.io/badge/Prefix Sum-前缀和-blue.svg">  


## Description - 题目描述

### EN:
<p>Given an integer array <code>nums</code>, return <em>an array</em> <code>answer</code> <em>such that</em> <code>answer[i]</code> <em>is equal to the product of all the elements of</em> <code>nums</code> <em>except</em> <code>nums[i]</code>.</p>

<p>The product of any prefix or suffix of <code>nums</code> is <strong>guaranteed</strong> to fit in a <strong>32-bit</strong> integer.</p>

<p>You must write an algorithm that runs in&nbsp;<code>O(n)</code>&nbsp;time and without using the division operation.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>
<pre><strong>Input:</strong> nums = [1,2,3,4]
<strong>Output:</strong> [24,12,8,6]
</pre><p><strong class="example">Example 2:</strong></p>
<pre><strong>Input:</strong> nums = [-1,1,0,-3,3]
<strong>Output:</strong> [0,0,9,0,0]
</pre>
<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>2 &lt;= nums.length &lt;= 10<sup>5</sup></code></li>
	<li><code>-30 &lt;= nums[i] &lt;= 30</code></li>
	<li>The product of any prefix or suffix of <code>nums</code> is <strong>guaranteed</strong> to fit in a <strong>32-bit</strong> integer.</li>
</ul>

<p>&nbsp;</p>
<p><strong>Follow up:</strong>&nbsp;Can you solve the problem in <code>O(1)&nbsp;</code>extra&nbsp;space complexity? (The output array <strong>does not</strong> count as extra space for space complexity analysis.)</p>


### ZH-CN:
<p>给你一个整数数组&nbsp;<code>nums</code>，返回 <em>数组&nbsp;<code>answer</code>&nbsp;，其中&nbsp;<code>answer[i]</code>&nbsp;等于&nbsp;<code>nums</code>&nbsp;中除&nbsp;<code>nums[i]</code>&nbsp;之外其余各元素的乘积</em>&nbsp;。</p>

<p>题目数据 <strong>保证</strong> 数组&nbsp;<code>nums</code>之中任意元素的全部前缀元素和后缀的乘积都在&nbsp; <strong>32 位</strong> 整数范围内。</p>

<p>请<strong>不要使用除法，</strong>且在&nbsp;<code>O(<em>n</em>)</code> 时间复杂度内完成此题。</p>

<p>&nbsp;</p>

<p><strong>示例 1:</strong></p>

<pre>
<strong>输入:</strong> nums = <code>[1,2,3,4]</code>
<strong>输出:</strong> <code>[24,12,8,6]</code>
</pre>

<p><strong>示例 2:</strong></p>

<pre>
<strong>输入:</strong> nums = [-1,1,0,-3,3]
<strong>输出:</strong> [0,0,9,0,0]
</pre>

<p>&nbsp;</p>

<p><strong>提示：</strong></p>

<ul>
	<li><code>2 &lt;= nums.length &lt;= 10<sup>5</sup></code></li>
	<li><code>-30 &lt;= nums[i] &lt;= 30</code></li>
	<li><strong>保证</strong> 数组&nbsp;<code>nums</code>之中任意元素的全部前缀元素和后缀的乘积都在&nbsp; <strong>32 位</strong> 整数范围内</li>
</ul>

<p>&nbsp;</p>

<p><strong>进阶：</strong>你可以在 <code>O(1)</code>&nbsp;的额外空间复杂度内完成这个题目吗？（ 出于对空间复杂度分析的目的，输出数组<strong>不被视为</strong>额外空间。）</p>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/product-of-array-except-self/description/)  -  [LeetCode-CN](https://leetcode.cn/problems/product-of-array-except-self/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| typescript  | 124 ms | 66.6 MB | 2023/03/25 19:57 |

```typescript

function productExceptSelf(nums: number[]): number[] {
  const ans: number[][] = new Array(nums.length).fill([]).map(i => [0, 0]);

  let acc = 1;

  for (let i = 0; i < nums.length; ++i) {
    ans[i][0] = acc * nums[i];
    acc = ans[i][0];
  }

  acc = 1;

  for (let i = nums.length - 1; i > 0; --i) {
    ans[i][1] = acc * nums[i];
    acc = ans[i][1];
  }

  return ans.map((i, idx) => {
    if (idx === 0) {
      return ans[1][1];
    }

    if (idx === nums.length - 1) {
      return ans[idx - 1][0];
    }

    return ans[idx-1][0] * ans[idx+1][1];
  })
};

```
## My Notes - 我的笔记


思路：
计算`nums[i]`左右累乘的数组乘积，再遍历一遍即可。
空间复杂度为`O(n)`。
```typescript
function productExceptSelf(nums: number[]): number[] {
  const ans: number[][] = new Array(nums.length).fill([]).map(i => [0, 0]);

  let acc = 1;

  for (let i = 0; i < nums.length; ++i) {
    ans[i][0] = acc * nums[i];
    acc = ans[i][0];
  }

  acc = 1;

  for (let i = nums.length - 1; i > 0; --i) {
    ans[i][1] = acc * nums[i];
    acc = ans[i][1];
  }

  return ans.map((i, idx) => {
    if (idx === 0) {
      return ans[1][1];
    }

    if (idx === nums.length - 1) {
      return ans[idx - 1][0];
    }

    return ans[idx-1][0] * ans[idx+1][1];
  })
};
```

