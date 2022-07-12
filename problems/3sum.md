
# 15. 3Sum - 三数之和

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Array-数组-blue.svg">   <img src="https://img.shields.io/badge/Two Pointers-双指针-blue.svg">   <img src="https://img.shields.io/badge/Sorting-排序-blue.svg">  


## Description - 题目描述

### EN:
<p>Given an integer array nums, return all the triplets <code>[nums[i], nums[j], nums[k]]</code> such that <code>i != j</code>, <code>i != k</code>, and <code>j != k</code>, and <code>nums[i] + nums[j] + nums[k] == 0</code>.</p>

<p>Notice that the solution set must not contain duplicate triplets.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>

<pre>
<strong>Input:</strong> nums = [-1,0,1,2,-1,-4]
<strong>Output:</strong> [[-1,-1,2],[-1,0,1]]
<strong>Explanation:</strong> 
nums[0] + nums[1] + nums[1] = (-1) + 0 + 1 = 0.
nums[1] + nums[2] + nums[4] = 0 + 1 + (-1) = 0.
nums[0] + nums[3] + nums[4] = (-1) + 2 + (-1) = 0.
The distinct triplets are [-1,0,1] and [-1,-1,2].
Notice that the order of the output and the order of the triplets does not matter.
</pre>

<p><strong>Example 2:</strong></p>

<pre>
<strong>Input:</strong> nums = [0,1,1]
<strong>Output:</strong> []
<strong>Explanation:</strong> The only possible triplet does not sum up to 0.
</pre>

<p><strong>Example 3:</strong></p>

<pre>
<strong>Input:</strong> nums = [0,0,0]
<strong>Output:</strong> [[0,0,0]]
<strong>Explanation:</strong> The only possible triplet sums up to 0.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>3 &lt;= nums.length &lt;= 3000</code></li>
	<li><code>-10<sup>5</sup> &lt;= nums[i] &lt;= 10<sup>5</sup></code></li>
</ul>


### ZH-CN:
<p>给你一个包含 <code>n</code> 个整数的数组 <code>nums</code>，判断 <code>nums</code> 中是否存在三个元素 <em>a，b，c ，</em>使得 <em>a + b + c = </em>0 ？请你找出所有和为 <code>0</code> 且不重复的三元组。</p>

<p><strong>注意：</strong>答案中不可以包含重复的三元组。</p>

<p> </p>

<p><strong>示例 1：</strong></p>

<pre>
<strong>输入：</strong>nums = [-1,0,1,2,-1,-4]
<strong>输出：</strong>[[-1,-1,2],[-1,0,1]]
</pre>

<p><strong>示例 2：</strong></p>

<pre>
<strong>输入：</strong>nums = []
<strong>输出：</strong>[]
</pre>

<p><strong>示例 3：</strong></p>

<pre>
<strong>输入：</strong>nums = [0]
<strong>输出：</strong>[]
</pre>

<p> </p>

<p><strong>提示：</strong></p>

<ul>
	<li><code>0 <= nums.length <= 3000</code></li>
	<li><code>-10<sup>5</sup> <= nums[i] <= 10<sup>5</sup></code></li>
</ul>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/3sum/description/)  -  [LeetCode-CN](https://leetcode.cn/problems/3sum/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| typescript  | 148 ms | 48.1 MB | 2021/11/03 22:37 |

```typescript

function threeSum(nums: number[]): number[][] {
  const len = nums.length; 
  if (len < 3) {
    return [];
  } else if (len === 3) {
    return nums[0]+nums[1]+nums[2] === 0 ? [nums] : [];
  }

  const sortedNums = [...nums].sort((a, b) => a - b);


  const ans: Array<Array<number>> = [];

  for (let idx = 0; idx < len; idx++) {
    if (sortedNums[0] > 0) {
      break;
    }

    const target = -sortedNums[idx];


    if (sortedNums[idx] === sortedNums[idx-1]) {
      continue;
    }

    let i = idx+1, j = len - 1;
    while (i < j) {
      if (sortedNums[i] + sortedNums[j] === target) {
        ans.push([sortedNums[idx], sortedNums[i], sortedNums[j]]);
        i++;
        j--;
        while (sortedNums[i] === sortedNums[i-1] && i < j) {
          i++;
        }
        while (sortedNums[j] === sortedNums[j+1] && i < j) {
          j--;
        }
      } else if (sortedNums[i] + sortedNums[j] < target) {
        i++;
      } else {
        j--;
      }
    }
  }
  return ans;
};

```
## My Notes - 我的笔记


**思路：**

排序后，从0到数组末尾遍历，固定一个 target，然后双指针在 target 后面寻找两数之和为 -target 的两个数字。

首指针为取 target 的索引 + 1， 尾指针为数组末尾。

遇到相加大于 -target 的，移动尾指针；小于 -target 时，移动首指针。等于 target 时，push 一个答案，首尾指针同时移动。

直到双指针碰头为止，开启下一轮循环。

注意：因为不可以包含重复的三元组，所以排序后的数组的元素遇到与它前面的元素重复时，跳过本轮循环。


