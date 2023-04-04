
# 312. Burst Balloons - 戳气球

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Array-数组-blue.svg">   <img src="https://img.shields.io/badge/Dynamic Programming-动态规划-blue.svg">  


## Description - 题目描述

### EN:
<p>You are given <code>n</code> balloons, indexed from <code>0</code> to <code>n - 1</code>. Each balloon is painted with a number on it represented by an array <code>nums</code>. You are asked to burst all the balloons.</p>

<p>If you burst the <code>i<sup>th</sup></code> balloon, you will get <code>nums[i - 1] * nums[i] * nums[i + 1]</code> coins. If <code>i - 1</code> or <code>i + 1</code> goes out of bounds of the array, then treat it as if there is a balloon with a <code>1</code> painted on it.</p>

<p>Return <em>the maximum coins you can collect by bursting the balloons wisely</em>.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input:</strong> nums = [3,1,5,8]
<strong>Output:</strong> 167
<strong>Explanation:</strong>
nums = [3,1,5,8] --&gt; [3,5,8] --&gt; [3,8] --&gt; [8] --&gt; []
coins =  3*1*5    +   3*5*8   +  1*3*8  + 1*8*1 = 167</pre>

<p><strong class="example">Example 2:</strong></p>

<pre>
<strong>Input:</strong> nums = [1,5]
<strong>Output:</strong> 10
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>n == nums.length</code></li>
	<li><code>1 &lt;= n &lt;= 300</code></li>
	<li><code>0 &lt;= nums[i] &lt;= 100</code></li>
</ul>


### ZH-CN:
<p>有 <code>n</code> 个气球，编号为<code>0</code> 到 <code>n - 1</code>，每个气球上都标有一个数字，这些数字存在数组&nbsp;<code>nums</code>&nbsp;中。</p>

<p>现在要求你戳破所有的气球。戳破第 <code>i</code> 个气球，你可以获得&nbsp;<code>nums[i - 1] * nums[i] * nums[i + 1]</code> 枚硬币。&nbsp;这里的 <code>i - 1</code> 和 <code>i + 1</code> 代表和&nbsp;<code>i</code>&nbsp;相邻的两个气球的序号。如果 <code>i - 1</code>或 <code>i + 1</code> 超出了数组的边界，那么就当它是一个数字为 <code>1</code> 的气球。</p>

<p>求所能获得硬币的最大数量。</p>

<p>&nbsp;</p>
<strong>示例 1：</strong>

<pre>
<strong>输入：</strong>nums = [3,1,5,8]
<strong>输出：</strong>167
<strong>解释：</strong>
nums = [3,1,5,8] --&gt; [3,5,8] --&gt; [3,8] --&gt; [8] --&gt; []
coins =  3*1*5    +   3*5*8   +  1*3*8  + 1*8*1 = 167</pre>

<p><strong>示例 2：</strong></p>

<pre>
<strong>输入：</strong>nums = [1,5]
<strong>输出：</strong>10
</pre>

<p>&nbsp;</p>

<p><strong>提示：</strong></p>

<ul>
	<li><code>n == nums.length</code></li>
	<li><code>1 &lt;= n &lt;= 300</code></li>
	<li><code>0 &lt;= nums[i] &lt;= 100</code></li>
</ul>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/burst-balloons/description/)  -  [LeetCode-CN](https://leetcode.cn/problems/burst-balloons/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| typescript  | 432 ms | 44.5 MB | 2023/04/04 19:58 |

```typescript

function maxCoins(nums: number[]): number {
  if (nums.length === 1) {
    return nums[0];
  }

  const n = nums.length;

  const newNum = new Array(n + 2).fill(0);

  newNum[0] = 1;
  newNum[newNum.length - 1] = 1;

  for (let i = 0; i < n; i++) {
    newNum[i + 1] = nums[i];
  }

  const mem = new Array(n + 2).fill([]).map(i => new Array(n + 2).fill(-1));


  const addOne = (start: number, end: number) => {
    if (start + 1 >= end) {
      mem[start][end] = 0;
      return 0;
    }

    if (mem[start][end] !== -1) {
      return mem[start][end];
    }

    let thisMax = -Infinity;

    for (let i = start + 1; i <= end - 1; i++) {
      const val = newNum[start] * newNum[i] * newNum[end] + addOne(start, i) + addOne(i, end);
      if (val > thisMax) {
        thisMax = val;
      }
    }

    mem[start][end] = thisMax;

    return thisMax;
  }

  return addOne(0, n + 1);

};

```
## My Notes - 我的笔记


递归+记忆化搜索：
```typescript
function maxCoins(nums: number[]): number {
  if (nums.length === 1) {
    return nums[0];
  }

  const n = nums.length;

  const newNum = new Array(n + 2).fill(0);

  newNum[0] = 1;
  newNum[newNum.length - 1] = 1;

  for (let i = 0; i < n; i++) {
    newNum[i + 1] = nums[i];
  }

  const mem = new Array(n + 2).fill([]).map(i => new Array(n + 2).fill(-1));


  const addOne = (start: number, end: number) => {
    if (start + 1 >= end) {
      mem[start][end] = 0;
      return 0;
    }

    if (mem[start][end] !== -1) {
      return mem[start][end];
    }

    let thisMax = -Infinity;

    for (let i = start + 1; i <= end - 1; i++) {
      const val = newNum[start] * newNum[i] * newNum[end] + addOne(start, i) + addOne(i, end);
      if (val > thisMax) {
        thisMax = val;
      }
    }

    mem[start][end] = thisMax;

    return thisMax;
  }

  return addOne(0, n + 1);

};Ï
```

