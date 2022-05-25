
# 4. Median of Two Sorted Arrays - 寻找两个正序数组的中位数

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Array-数组-blue.svg">   <img src="https://img.shields.io/badge/Binary Search-二分查找-blue.svg">   <img src="https://img.shields.io/badge/Divide and Conquer-分治-blue.svg">  


## Description - 题目描述

### EN:
<p>Given two sorted arrays <code>nums1</code> and <code>nums2</code> of size <code>m</code> and <code>n</code> respectively, return <strong>the median</strong> of the two sorted arrays.</p>

<p>The overall run time complexity should be <code>O(log (m+n))</code>.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>

<pre>
<strong>Input:</strong> nums1 = [1,3], nums2 = [2]
<strong>Output:</strong> 2.00000
<strong>Explanation:</strong> merged array = [1,2,3] and median is 2.
</pre>

<p><strong>Example 2:</strong></p>

<pre>
<strong>Input:</strong> nums1 = [1,2], nums2 = [3,4]
<strong>Output:</strong> 2.50000
<strong>Explanation:</strong> merged array = [1,2,3,4] and median is (2 + 3) / 2 = 2.5.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>nums1.length == m</code></li>
	<li><code>nums2.length == n</code></li>
	<li><code>0 &lt;= m &lt;= 1000</code></li>
	<li><code>0 &lt;= n &lt;= 1000</code></li>
	<li><code>1 &lt;= m + n &lt;= 2000</code></li>
	<li><code>-10<sup>6</sup> &lt;= nums1[i], nums2[i] &lt;= 10<sup>6</sup></code></li>
</ul>


### ZH-CN:
<p>给定两个大小分别为 <code>m</code> 和 <code>n</code> 的正序（从小到大）数组&nbsp;<code>nums1</code> 和&nbsp;<code>nums2</code>。请你找出并返回这两个正序数组的 <strong>中位数</strong> 。</p>

<p>算法的时间复杂度应该为 <code>O(log (m+n))</code> 。</p>

<p>&nbsp;</p>

<p><strong>示例 1：</strong></p>

<pre>
<strong>输入：</strong>nums1 = [1,3], nums2 = [2]
<strong>输出：</strong>2.00000
<strong>解释：</strong>合并数组 = [1,2,3] ，中位数 2
</pre>

<p><strong>示例 2：</strong></p>

<pre>
<strong>输入：</strong>nums1 = [1,2], nums2 = [3,4]
<strong>输出：</strong>2.50000
<strong>解释：</strong>合并数组 = [1,2,3,4] ，中位数 (2 + 3) / 2 = 2.5
</pre>

<p>&nbsp;</p>

<p>&nbsp;</p>

<p><strong>提示：</strong></p>

<ul>
	<li><code>nums1.length == m</code></li>
	<li><code>nums2.length == n</code></li>
	<li><code>0 &lt;= m &lt;= 1000</code></li>
	<li><code>0 &lt;= n &lt;= 1000</code></li>
	<li><code>1 &lt;= m + n &lt;= 2000</code></li>
	<li><code>-10<sup>6</sup> &lt;= nums1[i], nums2[i] &lt;= 10<sup>6</sup></code></li>
</ul>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/median-of-two-sorted-arrays/description/)  -  [LeetCode-CN](https://leetcode.cn/problems/median-of-two-sorted-arrays/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| javascript  | 104 ms | N/A | 2018/11/12 18:01 |

```javascript

/**
 * @param {number[]} nums1
 * @param {number[]} nums2
 * @return {number}
 */

var findMedianSortedArrays = function(nums1, nums2) {
    var sorted = [];
    var i=0, j=0;
    
    while (i < nums1.length && j < nums2.length) {
        if (nums1[i] <= nums2[j]) {
            sorted.push(nums1[i++]);
        } else {
            sorted.push(nums2[j++]);
        }
    }
    while(i < nums1.length) {
        sorted.push(nums1[i++]);
    }
    while(j < nums2.length) {
        sorted.push(nums2[j++]);
    }
    
    var len = sorted.length;
    
    if (len % 2 === 0) {
        return (sorted[len/2]+sorted[len/2-1])/2;
    } else {
        return sorted[Math.floor(len/2)];
    }
    
};

```
## My Notes - 我的笔记


这题用归并排序做应该是比较快而且比较好想的



## 寻找两个有序数组的中位数

### 方法1

num1和num2分别为两个数组，；要寻找这两个数组的中位数。

这个方法的思路先把num1和num2连接起来，再排序，然后分奇偶讨论。

如果数组长度是奇数，则排序过后数组的中位数为中间的数；

如果为偶数，则取中间两个数的平均值。

JavaScript内置的排序算法时间复杂度应该是O(log(n))。

```javascript
//比较两数大小的函数
function compare(value1, value2) {
    if (value1 < value2)
        return -1;
    else if (value1 > value2)
        return 1;
    else
        return 0;
}
var findMedianSortedArrays = function(nums1, nums2) {
    var connected = nums1.concat(nums2);
    var sorted = connected.sort(compare);
    var len = sorted.length;
    //console.log(sorted);
    if (len % 2 === 0) {
        return (sorted[len/2]+sorted[len/2-1])/2;
    } else {
        return sorted[Math.floor(len/2)];
    }
};
```

### 方法2

这个方法使用两个有序数组的归并。注意到num1和num2为有序数组，我们可以用时间复杂度为O(n)的归并算法来归并为一个数组。

归并的具体做法是两个指针在两个数组上走，如果第一个数组中的数小于或等于第二个数组中的数，则把第一个数组的数加入排序数组中，然后第一个数组指针后移一位；如果不是则加入第二个数，然后第二个数组指针后移一位。

其他思路与方法1相同。

``` javascript
var findMedianSortedArrays = function(nums1, nums2) {
    var sorted = [];
    var i=0, j=0;
    while (i < nums1.length && j < nums2.length) {
        if (nums1[i] <= nums2[j]) {
            sorted.push(nums1[i++]);
        } else {
            sorted.push(nums2[j++]);
        }
    }
    while(i < nums1.length) {
        sorted.push(nums1[i++]);
    }
    while(j < nums2.length) {
        sorted.push(nums2[j++]);
    }
    
    var len = sorted.length;
    if (len % 2 === 0) {
        return (sorted[len/2]+sorted[len/2-1])/2;
    } else {
        return sorted[Math.floor(len/2)];
    }
    
};
```

