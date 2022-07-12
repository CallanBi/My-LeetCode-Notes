
# 面试题40. 最小的k个数  LCOF - 最小的k个数

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Array-数组-blue.svg">   <img src="https://img.shields.io/badge/Divide and Conquer-分治-blue.svg">   <img src="https://img.shields.io/badge/Quickselect-快速选择-blue.svg">   <img src="https://img.shields.io/badge/Sorting-排序-blue.svg">   <img src="https://img.shields.io/badge/Heap (Priority Queue)-堆（优先队列）-blue.svg">  


## Description - 题目描述

### EN:
English description is not available for the problem. Please switch to Chinese.

### ZH-CN:
<p>输入整数数组 <code>arr</code> ，找出其中最小的 <code>k</code> 个数。例如，输入4、5、1、6、2、7、3、8这8个数字，则最小的4个数字是1、2、3、4。</p>

<p>&nbsp;</p>

<p><strong>示例 1：</strong></p>

<pre><strong>输入：</strong>arr = [3,2,1], k = 2
<strong>输出：</strong>[1,2] 或者 [2,1]
</pre>

<p><strong>示例 2：</strong></p>

<pre><strong>输入：</strong>arr = [0,1,2,1], k = 1
<strong>输出：</strong>[0]</pre>

<p>&nbsp;</p>

<p><strong>限制：</strong></p>

<ul>
	<li><code>0 &lt;= k &lt;= arr.length &lt;= 10000</code></li>
	<li><code>0 &lt;= arr[i]&nbsp;&lt;= 10000</code></li>
</ul>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/zui-xiao-de-kge-shu-lcof/description/)  -  [LeetCode-CN](https://leetcode.cn/problems/zui-xiao-de-kge-shu-lcof/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| typescript  | 92 ms | 42.7 MB | 2021/12/08 21:44 |

```typescript

function getLeastNumbers(arr: number[], k: number): number[] {
  if (k === arr.length || arr.length === 0) {
    return arr;
  }
  if (k === 0) {
    return [];
  }
  let start = 0, end = arr.length-1, idx = 0;
  while (idx !== k-1) {
    idx = partition(arr, start, end);
    if (idx > k-1) {
      end = idx - 1;
    } else if (idx < k-1) {
      start = idx + 1;
    } else {
      break;
    }
  }
  return arr.slice(0, k);
};

/**
 * @return 枢轴所在索引
 */
function partition(arr: number[], start: number, end: number): number {
  const pivot = arr[start];
  let i = start, j = end;

  while(i < j) {
    while (arr[j] >= pivot && i < j) {
      j--;
    }
    arr[i] = arr[j];
    while (arr[i] < pivot && i < j) {
      i++;
    }
    arr[j] = arr[i];
  }
  arr[i] = pivot;
  return i;
}

```
## My Notes - 我的笔记


# 最容易想到的解法：排序后slice 一下
时间复杂度为 `O(nlogn)`
```typescript
function getLeastNumbers(arr: number[], k: number): number[] {
  const sortedArr = arr.sort((a, b) => a - b);
  return sortedArr.slice(0, k);
};
```

# 一般解法：分治法
使用快排的 partition 思路；
当一趟 partition 后的枢轴所在索引比 `k-1` 要大时，继续对左边进行 partition；
当一趟 partition 后的枢轴所在索引比 `k-1` 要小时，继续对右边进行 partition；
直到枢轴所在索引和 `k-1` 相等时，返回数组切片即可。
允许改变原数组情况下可原地工作，不允许的情况下可以拷贝一份数组，需要额外的空间复杂度 `O(arr.length)`。
这个算法的时间复杂度是 `O(n)`, `n` 为数组长度。
```typescript
function getLeastNumbers(arr: number[], k: number): number[] {
  if (k === arr.length || arr.length === 0) {
    return arr;
  }
  if (k === 0) {
    return [];
  }
  let start = 0, end = arr.length-1, idx = 0;
  while (idx !== k-1) {
    idx = partition(arr, start, end);
    if (idx > k-1) {
      end = idx - 1;
    } else if (idx < k-1) {
      start = idx + 1;
    } else {
      break;
    }
  }
  return arr.slice(0, k);
};

/**
 * @return 枢轴所在索引
 */
function partition(arr: number[], start: number, end: number): number {
  const pivot = arr[start];
  let i = start, j = end;

  while(i < j) {
    while (arr[j] >= pivot && i < j) {
      j--;
    }
    arr[i] = arr[j];
    while (arr[i] < pivot && i < j) {
      i++;
    }
    arr[j] = arr[i];
  }
  arr[i] = pivot;
  return i;
}
```

# 第三种方法：使用优先队列
这种方法特别适合从海量数据中找出最大/最小的 k 个数据，即` arr.length` 很大，`k` 相对较小的情况。原因是在内存限制情况下，大批量数据不适合一次性读入内存中。所以我们用数据流来一个个地读取大批量数据。

其中，每次读取数据流时，取得最大值的时间复杂度是`O(1)`，插入的时间复杂度是 `O(logk)`。整个算法的时间复杂度是`O(nlogk)`。

其思路是利用优先队列（最大/最小堆）作为容器。

我们先启一个容量为 `k` 的容器，从海量数据流中读取数据。

当容器未满时，将数据放入容器；

当容器已满时，找到容器中最大的元素（对于最大堆，这个操作时间复杂度为 `O(1)`），与当前读取的元素进行比较；

若当前元素小于容器中最大元素，则删除容器中最大元素，插入当前元素；

若当前元素大于容器中最大元素，则当前元素不可能在最小的 k 个数的集合中。我们跳过当前元素，继续读入下一个元素。

直到整个数据流被读完为止。

这时，容器中的所有元素即是最小的 k 个数的集合。

在 Leetcode 中，JavaScript 环境自动引入了 lodash 和 [datastructures-js/priority-queue](https://github.com/datastructures-js/priority-queue)。我们直接用即可，无需显式 require 或 import。

```javascript
/**
 * @param {number[]} arr
 * @param {number} k
 * @return {number[]}
 */
var getLeastNumbers = function(arr, k) {
  if (k === arr.length || arr.length === 0) {
    return arr;
  }
  if (k === 0) {
    return [];
  }
  const priorityQueue = new MaxPriorityQueue();
  const len = arr.length;
  for(let i = 0; i < len; i++) {
    if (priorityQueue.size() < k) {
      priorityQueue.enqueue(arr[i]);
    } else {
      if (arr[i] < priorityQueue.front().element) {
        priorityQueue.dequeue();
        priorityQueue.enqueue(arr[i]);
      } else {
        continue;
      }
    }
  }
  return priorityQueue.toArray().map(e => e.element);
};
```





