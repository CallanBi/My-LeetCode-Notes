
# 912. Sort an Array - 排序数组

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Array-数组-blue.svg">   <img src="https://img.shields.io/badge/Divide and Conquer-分治-blue.svg">   <img src="https://img.shields.io/badge/Bucket Sort-桶排序-blue.svg">   <img src="https://img.shields.io/badge/Counting Sort-计数排序-blue.svg">   <img src="https://img.shields.io/badge/Radix Sort-基数排序-blue.svg">   <img src="https://img.shields.io/badge/Sorting-排序-blue.svg">   <img src="https://img.shields.io/badge/Heap (Priority Queue)-堆（优先队列）-blue.svg">   <img src="https://img.shields.io/badge/Merge Sort-归并排序-blue.svg">  


## Description - 题目描述

### EN:
<p>Given an array of integers <code>nums</code>, sort the array in ascending order.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>
<pre><strong>Input:</strong> nums = [5,2,3,1]
<strong>Output:</strong> [1,2,3,5]
</pre><p><strong>Example 2:</strong></p>
<pre><strong>Input:</strong> nums = [5,1,1,2,0,0]
<strong>Output:</strong> [0,0,1,1,2,5]
</pre>
<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= nums.length &lt;= 5 * 10<sup>4</sup></code></li>
	<li><code>-5 * 10<sup>4</sup> &lt;= nums[i] &lt;= 5 * 10<sup>4</sup></code></li>
</ul>


### ZH-CN:
<p>给你一个整数数组&nbsp;<code>nums</code>，请你将该数组升序排列。</p>

<p>&nbsp;</p>

<ol>
</ol>

<p><strong>示例 1：</strong></p>

<pre>
<strong>输入：</strong>nums = [5,2,3,1]
<strong>输出：</strong>[1,2,3,5]
</pre>

<p><strong>示例 2：</strong></p>

<pre>
<strong>输入：</strong>nums = [5,1,1,2,0,0]
<strong>输出：</strong>[0,0,1,1,2,5]
</pre>

<p>&nbsp;</p>

<p><strong>提示：</strong></p>

<ul>
	<li><code>1 &lt;= nums.length &lt;= 5 * 10<sup>4</sup></code></li>
	<li><code>-5 * 10<sup>4</sup> &lt;= nums[i] &lt;= 5 * 10<sup>4</sup></code></li>
</ul>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/sort-an-array/description/)  -  [LeetCode-CN](https://leetcode-cn.com/problems/sort-an-array/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| typescript  | 160 ms | 55.7 MB | 2021/04/05 0:23 |

```typescript

// 一趟快排的结果，返回结果和枢轴位置
const partition = (arr: number[]): [number[], number] => {
  const pivot = arr[0];
  const left = arr.filter(e => e < pivot);
  const pivotIdx = left.length;
  let hasSameFlag: boolean = false;
  const right = arr.filter(e => {
    if (e === pivot) {
      if (!hasSameFlag) {
        hasSameFlag = true;
        return false;
      } else {
        return true;
      }
    } else {
      return e >= pivot;
    }
  });
  return [[...left, pivot, ...right], pivotIdx];
}

const quickSort = (arr: number[]): number[] => {
  if (arr.length === 0) {
    return arr;
  }
  const [res, pivotIdx] = partition(arr);
  const pivot = res[pivotIdx];
  const left = quickSort(res.slice(0, pivotIdx));
  const right = quickSort(res.slice(pivotIdx + 1));
  return [...left, pivot, ...right];
}


function sortArray(nums: number[]): number[] {
  return quickSort(nums);
};

```
## My Notes - 我的笔记


# 先上经典解法
```typescript
// 一趟快排的划分（原地工作，改变数组）
const partition = (arr: number[], start: number, end: number): number => {
  // 选取第一个数字下标作为枢轴
  const pivotIdx = start;
  // 缓存枢轴上的数字
  const pivot = arr[pivotIdx];

  let startPtr = start;
  let endPtr = end;

  while (startPtr < endPtr) {
    while(arr[endPtr] >= pivot && startPtr < endPtr) {
      endPtr--;
    }

    arr[startPtr] = arr[endPtr];

    while(arr[startPtr] <= pivot && startPtr < endPtr) {
      startPtr++;
    }
    arr[endPtr] = arr[startPtr];
  }
  arr[startPtr] = pivot;
  return startPtr;
}

// 原地工作的快排算法
const quickSortInner = (nums: number[], start: number = 0, end: number = nums.length - 1): number[] => {
  if (start >= end) {
    return nums;
  }
  const pivotIdx = partition(nums, start, end);
  quickSortInner(nums, start, pivotIdx - 1);
  quickSortInner(nums, pivotIdx + 1, end);
}

const quickSort = (nums: number[]): number[] => {
  const numsCopy = [...nums];
  quickSortInner(numsCopy);
  return numsCopy;
};

function sortArray(nums: number[]): number[] {
  return quickSort(nums);
};
```
# partition
原地的快速排序是赋值，而不是交换。
当两个指针重合后，最终要把枢轴赋给该位置。
移动时，还要注意两个指针是否重合了。
如果选择第一个位置为枢轴，必须从高位开始。
当等于时，必须跳过而不是交换。
区分 `pivot` 和 `pivotIdx`。

# quickSortInner
由于是原地启动的快排，相当于改变了参数，所以不能这样写：
```typescript
const quickSort = (nums: number[], start: number = 0, end: number = nums.length - 1): number[] => {
	if (start >= end) {
    return nums;
  }
  const copy = [...nums];
  const pivotIdx = partition(nums, start, end);
  quickSortInner(nums, start, pivotIdx - 1);
  quickSortInner(nums, pivotIdx + 1, end);
  return copy;
};
```
因为调用栈永远保存是第一趟排序的结果，所以 copy 总是第一趟排序的结果。
注意加上停止递归的条件：
```typescript
if (start >= end) {
  return nums;
}
```
# 易于理解的方法
```
/**
 * 一趟快排的结果，返回结果和枢轴位置
 *  @params arr: number[] 原始数组
 *  @returns [number[], number] 一趟快排后的数组和枢轴位置
 */
const partition = (arr: number[]): [number[], number] => {
  const pivot = arr[0];
  const left = arr.filter(e => e < pivot);
  const pivotIdx = left.length;
  let hasSameFlag: boolean = false;
  const right = arr.filter(e => {
    // 当第一次遇到值和枢轴相同的元素，不将其加入 right，否则会重复
    if (e === pivot) {
      if (!hasSameFlag) {
        hasSameFlag = true;
        return false;
      } else {
        return true;
      }
    } else {
      return e >= pivot;
    }
  });
  return [[...left, pivot, ...right], pivotIdx];
}

const quickSort = (arr: number[]): number[] => {
  if (arr.length === 0) {
    return arr;
  }
  const [res, pivotIdx] = partition(arr);
  const pivot = res[pivotIdx];
  const left = quickSort(res.slice(0, pivotIdx));
  const right = quickSort(res.slice(pivotIdx + 1));
  return [...left, pivot, ...right];
}


function sortArray(nums: number[]): number[] {
  return quickSort(nums);
};
```

