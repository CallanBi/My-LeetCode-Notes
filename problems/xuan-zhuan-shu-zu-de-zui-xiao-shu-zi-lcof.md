
# 剑指 Offer 11. 旋转数组的最小数字  LCOF - 旋转数组的最小数字

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Array-数组-blue.svg">   <img src="https://img.shields.io/badge/Binary Search-二分查找-blue.svg">  


## Description - 题目描述

### EN:
English description is not available for the problem. Please switch to Chinese.

### ZH-CN:
<p>把一个数组最开始的若干个元素搬到数组的末尾，我们称之为数组的旋转。</p>

<p>给你一个可能存在&nbsp;<strong>重复</strong>&nbsp;元素值的数组&nbsp;<code>numbers</code>&nbsp;，它原来是一个升序排列的数组，并按上述情形进行了一次旋转。请返回旋转数组的<strong>最小元素</strong>。例如，数组&nbsp;<code>[3,4,5,1,2]</code> 为 <code>[1,2,3,4,5]</code> 的一次旋转，该数组的最小值为 1。&nbsp;&nbsp;</p>

<p>注意，数组 <code>[a[0], a[1], a[2], ..., a[n-1]]</code> 旋转一次 的结果为数组 <code>[a[n-1], a[0], a[1], a[2], ..., a[n-2]]</code> 。</p>

<p>&nbsp;</p>

<p><strong>示例 1：</strong></p>

<pre>
<strong>输入：</strong><code>numbers = </code>[3,4,5,1,2]
<strong>输出：</strong>1
</pre>

<p><strong>示例 2：</strong></p>

<pre>
<strong>输入：</strong><code>numbers = </code>[2,2,2,0,1]
<strong>输出：</strong>0
</pre>

<p>&nbsp;</p>

<p><strong>提示：</strong></p>

<ul>
	<li><code>n == numbers.length</code></li>
	<li><code>1 &lt;= n &lt;= 5000</code></li>
	<li><code>-5000 &lt;= numbers[i] &lt;= 5000</code></li>
	<li><code>numbers</code> 原来是一个升序排序的数组，并进行了 <code>1</code> 至 <code>n</code> 次旋转</li>
</ul>

<p>注意：本题与主站 154 题相同：<a href="https://leetcode-cn.com/problems/find-minimum-in-rotated-sorted-array-ii/">https://leetcode-cn.com/problems/find-minimum-in-rotated-sorted-array-ii/</a></p>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/xuan-zhuan-shu-zu-de-zui-xiao-shu-zi-lcof/description/)  -  [LeetCode-CN](https://leetcode.cn/problems/xuan-zhuan-shu-zu-de-zui-xiao-shu-zi-lcof/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| typescript  | 92 ms | 39.8 MB | 2021/10/10 22:22 |

```typescript

function minArray(numbers: number[]): number {
    let leftIdx = 0;
    let rightIdx = numbers.length - 1;
    // 没有旋转的特例
    if(numbers[leftIdx] < numbers[rightIdx]) {
        return numbers[leftIdx];
    }
    while (leftIdx <= rightIdx) {
        const midIdx = leftIdx + Math.floor((rightIdx - leftIdx) / 2);
        // 当直接找到分界线时，直接返回 mid
        if (numbers[midIdx-1] > numbers[midIdx]) {
            return numbers[midIdx];
        }
        if (numbers[midIdx] >= numbers[rightIdx]) {
            if (numbers[rightIdx] === numbers[leftIdx] && numbers[midIdx] === numbers[rightIdx]) {
                // 当 leftVal, rightVal, midVal 都是一样时，只能顺序查找
                return Math.min(...numbers);
            }
            // 说明mid在大的一方
            leftIdx = midIdx + 1;
        } else {
            // 说明 mid 在小的一方
            rightIdx = midIdx - 1;
        }
    }
    return numbers[leftIdx] ?? numbers[rightIdx];
};

```
## My Notes - 我的笔记


No notes

