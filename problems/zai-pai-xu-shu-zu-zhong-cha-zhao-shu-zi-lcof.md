
# 剑指 Offer 53 - I. 在排序数组中查找数字  LCOF - 在排序数组中查找数字 I

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Array-数组-blue.svg">   <img src="https://img.shields.io/badge/Binary Search-二分查找-blue.svg">  


## Description - 题目描述

### EN:
English description is not available for the problem. Please switch to Chinese.

### ZH-CN:
<p>统计一个数字在排序数组中出现的次数。</p>

<p> </p>

<p><strong>示例 1:</strong></p>

<pre>
<strong>输入:</strong> nums = [<code>5,7,7,8,8,10]</code>, target = 8
<strong>输出:</strong> 2</pre>

<p><strong>示例 2:</strong></p>

<pre>
<strong>输入:</strong> nums = [<code>5,7,7,8,8,10]</code>, target = 6
<strong>输出:</strong> 0</pre>

<p> </p>

<p><strong>提示：</strong></p>

<ul>
	<li><code>0 <= nums.length <= 10<sup>5</sup></code></li>
	<li><code>-10<sup>9</sup> <= nums[i] <= 10<sup>9</sup></code></li>
	<li><code>nums</code> 是一个非递减数组</li>
	<li><code>-10<sup>9</sup> <= target <= 10<sup>9</sup></code></li>
</ul>

<p> </p>

<p><strong>注意：</strong>本题与主站 34 题相同（仅返回值不同）：<a href="https://leetcode-cn.com/problems/find-first-and-last-position-of-element-in-sorted-array/">https://leetcode-cn.com/problems/find-first-and-last-position-of-element-in-sorted-array/</a></p>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/zai-pai-xu-shu-zu-zhong-cha-zhao-shu-zi-lcof/description/)  -  [LeetCode-CN](https://leetcode.cn/problems/zai-pai-xu-shu-zu-zhong-cha-zhao-shu-zi-lcof/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| typescript  | 84 ms | 41 MB | 2021/12/22 18:23 |

```typescript

function search(nums: number[], target: number): number {
  if (nums.length === 0) {
    return 0;
  }
  const firstIdx = divideFirst(nums, 0, nums.length-1, target);
  const lastIdx = divideLast(nums, 0, nums.length-1, target);

  return (firstIdx === -1 || lastIdx === -1) ? 0 : lastIdx - firstIdx + 1;
};


function divideFirst(nums: number[], start: number, end: number, target: number): number {
  if (start > end) {
    // 说明二分找完了都没找到，返回-1
    return -1;
  }
  const middleIdx = start + Math.floor((end - start) / 2);
  if (nums[middleIdx] === target) {
    if (nums[middleIdx - 1] === target) {
      return divideFirst(nums, start, middleIdx-1, target);
    } else {
      return middleIdx;
    }
  } else if (nums[middleIdx] > target) {
    return divideFirst(nums, start, middleIdx-1, target);
  } else {
    return divideFirst(nums, middleIdx+1, end, target);
  }
}

function divideLast(nums: number[], start: number, end: number, target: number): number {
  if (start > end) {
    // 说明二分找完了都没找到，返回-1
    return -1;
  }
  const middleIdx = start + Math.floor((end - start) / 2);
  if (nums[middleIdx] === target) {
    if (nums[middleIdx + 1] === target) {
      return divideLast(nums, middleIdx+1, end, target);
    } else {
      return middleIdx;
    }
  } else if (nums[middleIdx] > target) {
    return divideLast(nums, start, middleIdx-1, target);
  } else {
    return divideLast(nums, middleIdx+1, end, target);
  }
}

```
## My Notes - 我的笔记


典型的二分法（分治法）解决最快的题目。

看到排序数组，想到二分法。

注意：排序数组的二分法不是快排的 partition，二分法 divide 是查找排序数组中的数字，partition 是将非排序数组原地交换位置，构造成枢轴左边的数都小于（大于）枢轴，右边的数都大于（小于）枢轴的形式。


