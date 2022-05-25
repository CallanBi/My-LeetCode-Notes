
# 239. Sliding Window Maximum - 滑动窗口最大值

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Queue-队列-blue.svg">   <img src="https://img.shields.io/badge/Array-数组-blue.svg">   <img src="https://img.shields.io/badge/Sliding Window-滑动窗口-blue.svg">   <img src="https://img.shields.io/badge/Monotonic Queue-单调队列-blue.svg">   <img src="https://img.shields.io/badge/Heap (Priority Queue)-堆（优先队列）-blue.svg">  


## Description - 题目描述

### EN:
<p>You are given an array of integers&nbsp;<code>nums</code>, there is a sliding window of size <code>k</code> which is moving from the very left of the array to the very right. You can only see the <code>k</code> numbers in the window. Each time the sliding window moves right by one position.</p>

<p>Return <em>the max sliding window</em>.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>

<pre>
<strong>Input:</strong> nums = [1,3,-1,-3,5,3,6,7], k = 3
<strong>Output:</strong> [3,3,5,5,6,7]
<strong>Explanation:</strong> 
Window position                Max
---------------               -----
[1  3  -1] -3  5  3  6  7       <strong>3</strong>
 1 [3  -1  -3] 5  3  6  7       <strong>3</strong>
 1  3 [-1  -3  5] 3  6  7      <strong> 5</strong>
 1  3  -1 [-3  5  3] 6  7       <strong>5</strong>
 1  3  -1  -3 [5  3  6] 7       <strong>6</strong>
 1  3  -1  -3  5 [3  6  7]      <strong>7</strong>
</pre>

<p><strong>Example 2:</strong></p>

<pre>
<strong>Input:</strong> nums = [1], k = 1
<strong>Output:</strong> [1]
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= nums.length &lt;= 10<sup>5</sup></code></li>
	<li><code>-10<sup>4</sup> &lt;= nums[i] &lt;= 10<sup>4</sup></code></li>
	<li><code>1 &lt;= k &lt;= nums.length</code></li>
</ul>


### ZH-CN:
<p>给你一个整数数组 <code>nums</code>，有一个大小为&nbsp;<code>k</code><em>&nbsp;</em>的滑动窗口从数组的最左侧移动到数组的最右侧。你只可以看到在滑动窗口内的 <code>k</code>&nbsp;个数字。滑动窗口每次只向右移动一位。</p>

<p>返回 <em>滑动窗口中的最大值 </em>。</p>

<p>&nbsp;</p>

<p><strong>示例 1：</strong></p>

<pre>
<b>输入：</b>nums = [1,3,-1,-3,5,3,6,7], k = 3
<b>输出：</b>[3,3,5,5,6,7]
<b>解释：</b>
滑动窗口的位置                最大值
---------------               -----
[1  3  -1] -3  5  3  6  7       <strong>3</strong>
 1 [3  -1  -3] 5  3  6  7       <strong>3</strong>
 1  3 [-1  -3  5] 3  6  7      <strong> 5</strong>
 1  3  -1 [-3  5  3] 6  7       <strong>5</strong>
 1  3  -1  -3 [5  3  6] 7       <strong>6</strong>
 1  3  -1  -3  5 [3  6  7]      <strong>7</strong>
</pre>

<p><strong>示例 2：</strong></p>

<pre>
<b>输入：</b>nums = [1], k = 1
<b>输出：</b>[1]
</pre>

<p>&nbsp;</p>

<p><b>提示：</b></p>

<ul>
	<li><code>1 &lt;= nums.length &lt;= 10<sup>5</sup></code></li>
	<li><code>-10<sup>4</sup>&nbsp;&lt;= nums[i] &lt;= 10<sup>4</sup></code></li>
	<li><code>1 &lt;= k &lt;= nums.length</code></li>
</ul>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/sliding-window-maximum/description/)  -  [LeetCode-CN](https://leetcode-cn.com/problems/sliding-window-maximum/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| typescript  | 6236 ms | 79.3 MB | 2022/04/23 18:38 |

```typescript

function maxSlidingWindow(nums: number[], k: number): number[] {
  if (k === 1) {
    return nums;
  }

  const monotoneQueue: number[] = [], res: number[] = [];

  for (let i = 0; i < k; i++) {
    while (monotoneQueue[monotoneQueue.length - 1] !== undefined && monotoneQueue[monotoneQueue.length - 1] < nums[i]) {
      monotoneQueue.pop();
    }
    monotoneQueue.push(nums[i]);
  }

  if (nums[0] === monotoneQueue[0]) {
    const top = monotoneQueue.shift();
    res.push(top);
  } else {
    res.push(monotoneQueue[0]);
  }

  for (let i = k; i < nums.length; i++) {
    while (monotoneQueue[monotoneQueue.length - 1] !== undefined && monotoneQueue[monotoneQueue.length - 1] < nums[i]) {
      monotoneQueue.pop();
    }
    monotoneQueue.push(nums[i]);

    if (nums[i - k + 1] === monotoneQueue[0]) {
      const top = monotoneQueue.shift();
      res.push(top);
    } else {
      res.push(monotoneQueue[0]);
    }
  }

  return res;
};

```
## My Notes - 我的笔记


本题与 剑指 Offer 59 - I. 滑动窗口的最大值 相同，可参考那边的题解。

