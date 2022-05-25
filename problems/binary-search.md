
# 704. Binary Search - 二分查找

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Array-数组-blue.svg">   <img src="https://img.shields.io/badge/Binary Search-二分查找-blue.svg">  


## Description - 题目描述

### EN:
<p>Given an array of integers <code>nums</code> which is sorted in ascending order, and an integer <code>target</code>, write a function to search <code>target</code> in <code>nums</code>. If <code>target</code> exists, then return its index. Otherwise, return <code>-1</code>.</p>

<p>You must write an algorithm with <code>O(log n)</code> runtime complexity.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>

<pre>
<strong>Input:</strong> nums = [-1,0,3,5,9,12], target = 9
<strong>Output:</strong> 4
<strong>Explanation:</strong> 9 exists in nums and its index is 4
</pre>

<p><strong>Example 2:</strong></p>

<pre>
<strong>Input:</strong> nums = [-1,0,3,5,9,12], target = 2
<strong>Output:</strong> -1
<strong>Explanation:</strong> 2 does not exist in nums so return -1
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= nums.length &lt;= 10<sup>4</sup></code></li>
	<li><code>-10<sup>4</sup> &lt; nums[i], target &lt; 10<sup>4</sup></code></li>
	<li>All the integers in <code>nums</code> are <strong>unique</strong>.</li>
	<li><code>nums</code> is sorted in ascending order.</li>
</ul>


### ZH-CN:
<p>给定一个&nbsp;<code>n</code>&nbsp;个元素有序的（升序）整型数组&nbsp;<code>nums</code> 和一个目标值&nbsp;<code>target</code> &nbsp;，写一个函数搜索&nbsp;<code>nums</code>&nbsp;中的 <code>target</code>，如果目标值存在返回下标，否则返回 <code>-1</code>。</p>

<p><br>
<strong>示例 1:</strong></p>

<pre><strong>输入:</strong> <code>nums</code> = [-1,0,3,5,9,12], <code>target</code> = 9
<strong>输出:</strong> 4
<strong>解释:</strong> 9 出现在 <code>nums</code> 中并且下标为 4
</pre>

<p><strong>示例&nbsp;2:</strong></p>

<pre><strong>输入:</strong> <code>nums</code> = [-1,0,3,5,9,12], <code>target</code> = 2
<strong>输出:</strong> -1
<strong>解释:</strong> 2 不存在 <code>nums</code> 中因此返回 -1
</pre>

<p>&nbsp;</p>

<p><strong>提示：</strong></p>

<ol>
	<li>你可以假设 <code>nums</code>&nbsp;中的所有元素是不重复的。</li>
	<li><code>n</code>&nbsp;将在&nbsp;<code>[1, 10000]</code>之间。</li>
	<li><code>nums</code>&nbsp;的每个元素都将在&nbsp;<code>[-9999, 9999]</code>之间。</li>
</ol>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/binary-search/description/)  -  [LeetCode-CN](https://leetcode-cn.com/problems/binary-search/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| typescript  | 84 ms | 41.9 MB | 2021/04/08 0:48 |

```typescript

function search(nums: number[], target: number): number {
  // 找下界：
  // let left  = 0; 
  // let right = nums.length - 1;

  // while (left <= right) {
  //   let mid = left + Math.floor((right - left)/2);
  //   if (nums[mid] >= target) {
  //     // 找满足 x >= target 的第一个元素(下界)
  //     right = mid - 1;
  //   } else {
  //     left = mid + 1;
  //   }   
  // }
  // // 判断一下是否越界，或者不相等
  // if (left >= nums.length || nums[left] !== target) {
  //   // 找到下界后，判断是否存在
  //   return -1;
  // }

  // return left;

  // 找上界：
  let left  = 0; 
  let right = nums.length - 1;

  while (left <= right) {
    let mid = left + Math.floor((right - left)/2);
    if (nums[mid] > target) {
      // 找满足 x <= target 的最后一个元素(上界)
      right = mid - 1;
    } else {
      left = mid + 1;
    }   
  }
  // 判断一下是否越界，或者不相等
  if (right< 0 || nums[right] !== target) {
    // 找到下界后，判断是否存在
    return -1;
  }

  return right;
  
};

```
## My Notes - 我的笔记


# 两种思路
## 找下界(以此为准)
```typescript
let left  = 0; 
  let right = nums.length - 1;

  while (left <= right) {
    let mid = left + Math.floor((right - left)/2);
    if (nums[mid] >= target) {
      // 找满足 nums[mid] >= target 的第一个元素(下界)
      right = mid - 1;
    } else {
      left = mid + 1;
    }   
  }
  // 判断一下是否越界，或者不相等
  if (left >= nums.length || nums[left] !== target) {
    // 找到下界后，判断是否存在
    return -1;
  }

  return left;
```

## 找上界
```typescript
  let left  = 0; 
  let right = nums.length - 1;

  while (left <= right) {
    let mid = left + Math.floor((right - left)/2);
    if (nums[mid] <= target) {
			 left = mid + 1;
      // 找满足 x <= target 的最后一个元素(上界)
    } else {
			right = mid - 1;
    }   
  }
  // 判断一下是否越界，或者不相等
  if (right< 0 || nums[right] !== target) {
    // 找到下界后，判断是否存在
    return -1;
  }

  return right;
```

[参考](https://imageslr.github.io/2020/03/15/binary-search.html)

