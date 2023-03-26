
# 287. Find the Duplicate Number - 寻找重复数

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Bit Manipulation-位运算-blue.svg">   <img src="https://img.shields.io/badge/Array-数组-blue.svg">   <img src="https://img.shields.io/badge/Two Pointers-双指针-blue.svg">   <img src="https://img.shields.io/badge/Binary Search-二分查找-blue.svg">  


## Description - 题目描述

### EN:
<p>Given an array of integers <code>nums</code> containing&nbsp;<code>n + 1</code> integers where each integer is in the range <code>[1, n]</code> inclusive.</p>

<p>There is only <strong>one repeated number</strong> in <code>nums</code>, return <em>this&nbsp;repeated&nbsp;number</em>.</p>

<p>You must solve the problem <strong>without</strong> modifying the array <code>nums</code>&nbsp;and uses only constant extra space.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input:</strong> nums = [1,3,4,2,2]
<strong>Output:</strong> 2
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre>
<strong>Input:</strong> nums = [3,1,3,4,2]
<strong>Output:</strong> 3
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= n &lt;= 10<sup>5</sup></code></li>
	<li><code>nums.length == n + 1</code></li>
	<li><code>1 &lt;= nums[i] &lt;= n</code></li>
	<li>All the integers in <code>nums</code> appear only <strong>once</strong> except for <strong>precisely one integer</strong> which appears <strong>two or more</strong> times.</li>
</ul>

<p>&nbsp;</p>
<p><b>Follow up:</b></p>

<ul>
	<li>How can we prove that at least one duplicate number must exist in <code>nums</code>?</li>
	<li>Can you solve the problem in linear runtime complexity?</li>
</ul>


### ZH-CN:
<p>给定一个包含&nbsp;<code>n + 1</code> 个整数的数组&nbsp;<code>nums</code> ，其数字都在&nbsp;<code>[1, n]</code>&nbsp;范围内（包括 <code>1</code> 和 <code>n</code>），可知至少存在一个重复的整数。</p>

<p>假设 <code>nums</code> 只有 <strong>一个重复的整数</strong> ，返回&nbsp;<strong>这个重复的数</strong> 。</p>

<p>你设计的解决方案必须 <strong>不修改</strong> 数组 <code>nums</code> 且只用常量级 <code>O(1)</code> 的额外空间。</p>

<p>&nbsp;</p>

<p><strong>示例 1：</strong></p>

<pre>
<strong>输入：</strong>nums = [1,3,4,2,2]
<strong>输出：</strong>2
</pre>

<p><strong>示例 2：</strong></p>

<pre>
<strong>输入：</strong>nums = [3,1,3,4,2]
<strong>输出：</strong>3
</pre>

<p>&nbsp;</p>

<p><strong>提示：</strong></p>

<ul>
	<li><code>1 &lt;= n &lt;= 10<sup>5</sup></code></li>
	<li><code>nums.length == n + 1</code></li>
	<li><code>1 &lt;= nums[i] &lt;= n</code></li>
	<li><code>nums</code> 中 <strong>只有一个整数</strong> 出现 <strong>两次或多次</strong> ，其余整数均只出现 <strong>一次</strong></li>
</ul>

<p>&nbsp;</p>

<p><b>进阶：</b></p>

<ul>
	<li>如何证明 <code>nums</code> 中至少存在一个重复的数字?</li>
	<li>你可以设计一个线性级时间复杂度 <code>O(n)</code> 的解决方案吗？</li>
</ul>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/find-the-duplicate-number/description/)  -  [LeetCode-CN](https://leetcode.cn/problems/find-the-duplicate-number/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| typescript  | 80 ms | 50.6 MB | 2023/03/26 11:26 |

```typescript

function findDuplicate(nums: number[]): number {
  let slow = nums[nums[0]], fast = nums[nums[nums[0]]];
  while (slow !== fast) {
    slow = nums[slow];
    fast = nums[nums[fast]];
  }

  slow = nums[0];

  while (slow !== fast) {
    slow = nums[slow];
    fast = nums[fast];
  }

  return slow;
};

```
## My Notes - 我的笔记


注意：投票法是寻找超过数组一半的多数元素，不要搞混了。
# 可以改变原数组
如果可以改变原数组，则可以这样：
因为数组都在$[1, n]$范围，长度为$n+1$，我们可以不断交换`nums[0]`和`nums[nums[0]]`，直到找到一个`nums[nums[0]] === nums[0]`，则这个 `nums[0]`即为重复的数。
```typescript
function findDuplicate(nums: number[]): number {
  while (true) {
    const temp = nums[nums[0]];
    if (nums[nums[0]] === nums[0]) {
      return nums[0];
    }
    nums[nums[0]] = nums[0];
    nums[0] = temp;
  }
};
```

# 不可改变原数组
沿着 $i -> nums[i]$ 可构建一个图，有重复数该图有环。
等价与寻找一个图的环。

```typescript
function findDuplicate(nums: number[]): number {
  let slow = nums[nums[0]], fast = nums[nums[nums[0]]];
  while (slow !== fast) {
    slow = nums[slow];
    fast = nums[nums[fast]];
  }

  slow = nums[0];

  while (slow !== fast) {
    slow = nums[slow];
    fast = nums[fast];
  }

  return slow;
};
```

