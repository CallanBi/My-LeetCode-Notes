
# 31. Next Permutation - 下一个排列

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Array-数组-blue.svg">   <img src="https://img.shields.io/badge/Two Pointers-双指针-blue.svg">  


## Description - 题目描述

### EN:
<p>A <strong>permutation</strong> of an array of integers is an arrangement of its members into a sequence or linear order.</p>

<ul>
	<li>For example, for <code>arr = [1,2,3]</code>, the following are all the permutations of <code>arr</code>: <code>[1,2,3], [1,3,2], [2, 1, 3], [2, 3, 1], [3,1,2], [3,2,1]</code>.</li>
</ul>

<p>The <strong>next permutation</strong> of an array of integers is the next lexicographically greater permutation of its integer. More formally, if all the permutations of the array are sorted in one container according to their lexicographical order, then the <strong>next permutation</strong> of that array is the permutation that follows it in the sorted container. If such arrangement is not possible, the array must be rearranged as the lowest possible order (i.e., sorted in ascending order).</p>

<ul>
	<li>For example, the next permutation of <code>arr = [1,2,3]</code> is <code>[1,3,2]</code>.</li>
	<li>Similarly, the next permutation of <code>arr = [2,3,1]</code> is <code>[3,1,2]</code>.</li>
	<li>While the next permutation of <code>arr = [3,2,1]</code> is <code>[1,2,3]</code> because <code>[3,2,1]</code> does not have a lexicographical larger rearrangement.</li>
</ul>

<p>Given an array of integers <code>nums</code>, <em>find the next permutation of</em> <code>nums</code>.</p>

<p>The replacement must be <strong><a href="http://en.wikipedia.org/wiki/In-place_algorithm" target="_blank">in place</a></strong> and use only constant extra memory.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input:</strong> nums = [1,2,3]
<strong>Output:</strong> [1,3,2]
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre>
<strong>Input:</strong> nums = [3,2,1]
<strong>Output:</strong> [1,2,3]
</pre>

<p><strong class="example">Example 3:</strong></p>

<pre>
<strong>Input:</strong> nums = [1,1,5]
<strong>Output:</strong> [1,5,1]
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= nums.length &lt;= 100</code></li>
	<li><code>0 &lt;= nums[i] &lt;= 100</code></li>
</ul>


### ZH-CN:
<p>整数数组的一个 <strong>排列</strong>&nbsp; 就是将其所有成员以序列或线性顺序排列。</p>

<ul>
	<li>例如，<code>arr = [1,2,3]</code> ，以下这些都可以视作 <code>arr</code> 的排列：<code>[1,2,3]</code>、<code>[1,3,2]</code>、<code>[3,1,2]</code>、<code>[2,3,1]</code> 。</li>
</ul>

<p>整数数组的 <strong>下一个排列</strong> 是指其整数的下一个字典序更大的排列。更正式地，如果数组的所有排列根据其字典顺序从小到大排列在一个容器中，那么数组的 <strong>下一个排列</strong> 就是在这个有序容器中排在它后面的那个排列。如果不存在下一个更大的排列，那么这个数组必须重排为字典序最小的排列（即，其元素按升序排列）。</p>

<ul>
	<li>例如，<code>arr = [1,2,3]</code> 的下一个排列是 <code>[1,3,2]</code> 。</li>
	<li>类似地，<code>arr = [2,3,1]</code> 的下一个排列是 <code>[3,1,2]</code> 。</li>
	<li>而 <code>arr = [3,2,1]</code> 的下一个排列是 <code>[1,2,3]</code> ，因为 <code>[3,2,1]</code> 不存在一个字典序更大的排列。</li>
</ul>

<p>给你一个整数数组 <code>nums</code> ，找出 <code>nums</code> 的下一个排列。</p>

<p>必须<strong><a href="https://baike.baidu.com/item/%E5%8E%9F%E5%9C%B0%E7%AE%97%E6%B3%95" target="_blank"> 原地 </a></strong>修改，只允许使用额外常数空间。</p>

<p>&nbsp;</p>

<p><strong>示例 1：</strong></p>

<pre>
<strong>输入：</strong>nums = [1,2,3]
<strong>输出：</strong>[1,3,2]
</pre>

<p><strong>示例 2：</strong></p>

<pre>
<strong>输入：</strong>nums = [3,2,1]
<strong>输出：</strong>[1,2,3]
</pre>

<p><strong>示例 3：</strong></p>

<pre>
<strong>输入：</strong>nums = [1,1,5]
<strong>输出：</strong>[1,5,1]
</pre>

<p>&nbsp;</p>

<p><strong>提示：</strong></p>

<ul>
	<li><code>1 &lt;= nums.length &lt;= 100</code></li>
	<li><code>0 &lt;= nums[i] &lt;= 100</code></li>
</ul>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/next-permutation/description/)  -  [LeetCode-CN](https://leetcode.cn/problems/next-permutation/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| typescript  | 68 ms | 43.8 MB | 2022/05/03 17:25 |

```typescript

/**
 Do not return anything, modify nums in-place instead.
 */
function nextPermutation(nums: number[]): void {
  if (nums.length === 1) {
    return;
  }

  const len = nums.length;

  let rightPrev = nums[len - 1];

  let i = len - 2;

  for (; i >= 0; i--) {
    if (nums[i] >= rightPrev) {
      rightPrev = nums[i];
    } else {
      break;
    }
  }

  if (i === -1) {
    reverse(nums, 0);
    return;
  }

  const pivot = i;

  i = len - 1;

  for (; i >= 0; i--) {
    if (nums[i] > nums[pivot]) {
      break;
    } 
  }

  [nums[pivot], nums[i]] = [nums[i], nums[pivot]];

  reverse(nums, pivot+1);
};

/** in-place reverse, start variable stands for the starting index */
function reverse(nums: number[], start: number) {
  if (nums.length - start === 0 || nums.length - start === 1) {
    return;
  }

  let i = start, j = nums.length - 1;

  while (i < j) {
    [nums[i], nums[j]] = [nums[j], nums[i]];
    i++;
    j--;
  }
}

```
## My Notes - 我的笔记


参考[这篇文章](https://www.nayuki.io/page/next-lexicographical-permutation-algorithm)，详细描述了下一个排列的算法。这个东西其实在 C++ 标准库中有实现，需要了解。

下面是这篇文章的一些摘抄。

# Next lexicographical permutation algorithm

## Introduction

Suppose we have a finite sequence of numbers like (0, 3, 3, 5, 8), and want to generate all its permutations. What is the best way to do so?

The naive way would be to take a top-down, recursive approach. We could pick the first element, then recurse and pick the second element from the remaining ones, and so on. But this method is tricky because it involves recursion, stack storage, and skipping over duplicate values. Moreover, if we insist on manipulating the sequence in place (without producing temporary arrays), then it’s difficult to generate the permutations in lexicographical order.

It turns out that the best approach to generating all the permutations is to start at the lowest permutation, and repeatedly compute the next permutation in place. The simple and fast algorithm for performing this is what will be described on this page. We will use concrete examples to illustrate the reasoning behind each step of the algorithm.

## The algorithm

[![Next permutation algorithm](https://www.nayuki.io/res/next-lexicographical-permutation-algorithm/next-permutation-algorithm.svg "Next permutation algorithm")](https://www.nayuki.io/res/next-lexicographical-permutation-algorithm/next-permutation-algorithm.svg)

We will use the sequence (0, 1, 2, 5, 3, 3, 0) as a running example.

The key observation in this algorithm is that when we want to compute the next permutation, we must “increase” the sequence *as little as possible*. Just like when we count up using numbers, we try to modify the rightmost elements and leave the left side unchanged. For example, there is no need to change the first element from 0 to 1, because by changing the prefix from (0, 1) to (0, 2) we get an even closer next permutation. In fact, there is no need to change the second element either, which brings us to the next point.

Firstly, identify the longest suffix that is non-increasing (i.e. weakly decreasing). In our example, the suffix with this property is (5, 3, 3, 0). This suffix is already the highest permutation, so we can’t make a next permutation just by modifying it – we need to modify some element(s) to the left of it. (Note that we can identify this suffix in Θ(*n*) time by scanning the sequence from right to left. Also note that such a suffix has at least one element, because a single element substring is trivially non-increasing.)

Secondly, look at the element immediately to the left of the suffix (in the example it’s 2) and call it the pivot. (If there is no such element – i.e. the entire sequence is non-increasing – then this is already the last permutation.) The pivot is necessarily less than the head of the suffix (in the example it’s 5). So some element in the suffix is greater than the pivot. If we swap the pivot with the smallest element in the suffix that is greater than the pivot, then the prefix is minimally increased. (The prefix is everything in the sequence except the suffix.) In the example, we end up with the new prefix (0, 1, 3) and new suffix (5, 3, 2, 0). (Note that if the suffix has multiple copies of the new pivot, we should take the rightmost copy – this plays into the next step.)

Finally, we sort the suffix in non-decreasing (i.e. weakly increasing) order because we increased the prefix, so we want to make the new suffix as low as possible. In fact, we can avoid sorting and simply reverse the suffix, because the replaced element respects the weakly decreasing order. Thus we obtain the sequence (0, 1, 3, 0, 2, 3, 5), which is the next permutation that we wanted to compute.

Condensed mathematical description:

1.  Find largest index *i* such that *array*\[*i* − 1] < *array*\[*i*].\
    (If no such *i* exists, then this is already the last permutation.)

2.  Find largest index *j* such that j ≥ i and *array*\[*j*] > *array*\[*i* − 1].

3.  Swap *array*\[*j*] and *array*\[*i* − 1].

4.  Reverse the suffix starting at *array*\[*i*].

Overall, this algorithm to compute the next lexicographical permutation has Θ(*n*) worst-case time complexity, and Θ(1) space complexity. Thus, computing every permutation requires Θ(*n*! × *n*) run time.

Now if you truly understand the algorithm, here’s an extension exercise for you: Design the algorithm for stepping backward to the *previous* lexicographical permutation. (Spoilers at the bottom.)

# 我基于此写的代码

```typescript
/**
 Do not return anything, modify nums in-place instead.
 */
function nextPermutation(nums: number[]): void {
  if (nums.length === 1) {
    return;
  }

  const len = nums.length;

  let rightPrev = nums[len - 1];

  let i = len - 2;

  for (; i >= 0; i--) {
    if (nums[i] >= rightPrev) {
      rightPrev = nums[i];
    } else {
      break;
    }
  }

  if (i === -1) {
    reverse(nums, 0);
    return;
  }

  const pivot = i;

  i = len - 1;

  for (; i >= 0; i--) {
    if (nums[i] > nums[pivot]) {
      break;
    } 
  }

  [nums[pivot], nums[i]] = [nums[i], nums[pivot]];

  reverse(nums, pivot+1);
};

/** in-place reverse, start variable stands for the starting index */
function reverse(nums: number[], start: number) {
  if (nums.length - start === 0 || nums.length - start === 1) {
    return;
  }

  let i = start, j = nums.length - 1;

  while (i < j) {
    [nums[i], nums[j]] = [nums[j], nums[i]];
    i++;
    j--;
  }
}
```


