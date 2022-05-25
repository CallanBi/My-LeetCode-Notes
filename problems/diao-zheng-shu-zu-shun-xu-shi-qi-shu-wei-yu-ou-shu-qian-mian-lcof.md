
# 剑指 Offer 21. 调整数组顺序使奇数位于偶数前面 LCOF - 调整数组顺序使奇数位于偶数前面

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Array-数组-blue.svg">   <img src="https://img.shields.io/badge/Two Pointers-双指针-blue.svg">   <img src="https://img.shields.io/badge/Sorting-排序-blue.svg">  


## Description - 题目描述

### EN:
<p>English description is not available for the problem. Please switch to Chinese.</p>


### ZH-CN:
<p>输入一个整数数组，实现一个函数来调整该数组中数字的顺序，使得所有奇数在数组的前半部分，所有偶数在数组的后半部分。</p>

<p>&nbsp;</p>

<p><strong>示例：</strong></p>

<pre>
<strong>输入：</strong>nums =&nbsp;[1,2,3,4]
<strong>输出：</strong>[1,3,2,4] 
<strong>注：</strong>[3,1,2,4] 也是正确的答案之一。</pre>

<p>&nbsp;</p>

<p><strong>提示：</strong></p>

<ol>
	<li><code>0 &lt;= nums.length &lt;= 50000</code></li>
	<li><code>0 &lt;= nums[i] &lt;= 10000</code></li>
</ol>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/diao-zheng-shu-zu-shun-xu-shi-qi-shu-wei-yu-ou-shu-qian-mian-lcof/description/)  -  [LeetCode-CN](https://leetcode.cn/problems/diao-zheng-shu-zu-shun-xu-shi-qi-shu-wei-yu-ou-shu-qian-mian-lcof/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| typescript  | 92 ms | 45.4 MB | 2021/11/04 12:52 |

```typescript

function exchange(nums: number[]): number[] {
  let front = 0, rear = nums.length - 1;
  while (front < rear) {
    while (nums[front] % 2 === 1 && nums[rear] % 2 === 0) {
      front++;
      rear--;
    }
    // 都为奇数
    while(nums[front] % 2 === 1 && nums[rear] % 2 === 1 && front < rear) {
      front++;
    }
    // 都为偶数
    while(nums[front] % 2 === 0 && nums[rear] % 2 === 0 && front < rear) {
      rear--;
    }
    if (nums[front] % 2 === 0 && nums[rear] % 2 === 1 && front < rear) {
      const temp = nums[front];
      nums[front] = nums[rear];
      nums[rear] = temp;
      front++;
      rear--;
    }
  }
  return nums;
};

```
## My Notes - 我的笔记


No notes

