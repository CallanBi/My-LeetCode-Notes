
# 剑指 Offer 51. 数组中的逆序对  LCOF - 数组中的逆序对

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Binary Indexed Tree-树状数组-blue.svg">   <img src="https://img.shields.io/badge/Segment Tree-线段树-blue.svg">   <img src="https://img.shields.io/badge/Array-数组-blue.svg">   <img src="https://img.shields.io/badge/Binary Search-二分查找-blue.svg">   <img src="https://img.shields.io/badge/Divide and Conquer-分治-blue.svg">   <img src="https://img.shields.io/badge/Ordered Set-有序集合-blue.svg">   <img src="https://img.shields.io/badge/Merge Sort-归并排序-blue.svg">  


## Description - 题目描述

### EN:
English description is not available for the problem. Please switch to Chinese.

### ZH-CN:
<p>在数组中的两个数字，如果前面一个数字大于后面的数字，则这两个数字组成一个逆序对。输入一个数组，求出这个数组中的逆序对的总数。</p>

<p>&nbsp;</p>

<p><strong>示例 1:</strong></p>

<pre><strong>输入</strong>: [7,5,6,4]
<strong>输出</strong>: 5</pre>

<p>&nbsp;</p>

<p><strong>限制：</strong></p>

<p><code>0 &lt;= 数组长度 &lt;= 50000</code></p>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/shu-zu-zhong-de-ni-xu-dui-lcof/description/)  -  [LeetCode-CN](https://leetcode-cn.com/problems/shu-zu-zhong-de-ni-xu-dui-lcof/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| javascript  | 156 ms | 51.3 MB | 2021/12/21 23:38 |

```javascript

/**
 * @param {number[]} nums
 * @return {number}
 */
var reversePairs = function(nums) {
  if (nums.length === 0) {
    return 0;
  }
  return mergeSortCore(nums, 0, nums.length-1); // 允许改变原数组的话可以这样写
};

const mergeSortCore = (arr, start, end) => {
  if (start === end) {
    return 0;
  }

  const splitedIdx = start + Math.floor((end - start) / 2);
  const leftNum = mergeSortCore(arr, start, splitedIdx);
  const rightNum = mergeSortCore(arr, splitedIdx+1, end);
  
  let res = leftNum + rightNum;

  let i = start, j = splitedIdx + 1;
  const temp = [];
  while (i <= splitedIdx && j <= end) {
    while (arr[i] <= arr[j] && i <= splitedIdx && j <= end) {
      temp.push(arr[i]);
      i++;
    }
    while (arr[i] > arr[j] && i <= splitedIdx && j <= end) {
      temp.push(arr[j]);
      res += splitedIdx - i + 1;
      j++;
    }
  }

  while (i <= splitedIdx) {
    temp.push(arr[i]);
    i++;
  }
  
  while (j <= end) {
    temp.push(arr[j]);
    j++;
  }

  for (let i = start; i <= end; i++) {
    arr[i] = temp[i - start]; // 这里不能用 temp.shift(), 因为 shift()要整体移动数组，时间复杂度为 O(n)
  }

  return res;
}

```
## My Notes - 我的笔记


**思路：**

归并排序的应用。对于输入的数组进行递归的归并原地排序。

指定一个 `splitedIdx`，对于左边和右边分别进行归并排序，同时统计左边和右边的逆序对。这时就得到了两个有序数组和左边和右边各自的逆序对数量。

再对这两个有序数组排序，即有序链表的排序。排序的同时统计逆序对数量即可。

**关键点：**

1.  归并排序过程中，逆序对顺序需要画图想好细节再写代码

2.  `Array.prototype.shift()` 世界复杂度太高，最好不用

3.  合并两个有序链表，在移动指针的循环中，也要交上最外层循环的条件`i <= splitedIdx && j <= end`

```javascript
/**
 * @param {number[]} nums
 * @return {number}
 */
var reversePairs = function(nums) {
  if (nums.length === 0) {
    return 0;
  }
  return mergeSortCore(nums, 0, nums.length-1); // 允许改变原数组的话可以这样写
};

const mergeSortCore = (arr, start, end) => {
  if (start === end) {
    return 0;
  }

  const splitedIdx = start + Math.floor((end - start) / 2);
  const leftNum = mergeSortCore(arr, start, splitedIdx);
  const rightNum = mergeSortCore(arr, splitedIdx+1, end);
  
  let res = leftNum + rightNum;

  let i = start, j = splitedIdx + 1;
  const temp = [];
  while (i <= splitedIdx && j <= end) {
    while (arr[i] <= arr[j] && i <= splitedIdx && j <= end) {
      temp.push(arr[i]);
      i++;
    }
    while (arr[i] > arr[j] && i <= splitedIdx && j <= end) {
      temp.push(arr[j]);
      res += splitedIdx - i + 1; // 这句很关键，要想明白逆序对怎么算，画个图，应该是累加左边的
      j++;
    }
  }

  while (i <= splitedIdx) {
    temp.push(arr[i]);
    i++;
  }
  
  while (j <= end) {
    temp.push(arr[j]);
    j++;
  }

  for (let i = start; i <= end; i++) {
    arr[i] = temp[i - start]; // 这里不能用 temp.shift(), 因为 shift()要整体移动数组，时间复杂度为 O(n)
  }

  return res;
}
```


