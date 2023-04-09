
# 347. Top K Frequent Elements - 前 K 个高频元素

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Array-数组-blue.svg">   <img src="https://img.shields.io/badge/Hash Table-哈希表-blue.svg">   <img src="https://img.shields.io/badge/Divide and Conquer-分治-blue.svg">   <img src="https://img.shields.io/badge/Bucket Sort-桶排序-blue.svg">   <img src="https://img.shields.io/badge/Counting-计数-blue.svg">   <img src="https://img.shields.io/badge/Quickselect-快速选择-blue.svg">   <img src="https://img.shields.io/badge/Sorting-排序-blue.svg">   <img src="https://img.shields.io/badge/Heap (Priority Queue)-堆（优先队列）-blue.svg">  


## Description - 题目描述

### EN:
<p>Given an integer array <code>nums</code> and an integer <code>k</code>, return <em>the</em> <code>k</code> <em>most frequent elements</em>. You may return the answer in <strong>any order</strong>.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>
<pre><strong>Input:</strong> nums = [1,1,1,2,2,3], k = 2
<strong>Output:</strong> [1,2]
</pre><p><strong class="example">Example 2:</strong></p>
<pre><strong>Input:</strong> nums = [1], k = 1
<strong>Output:</strong> [1]
</pre>
<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= nums.length &lt;= 10<sup>5</sup></code></li>
	<li><code>-10<sup>4</sup> &lt;= nums[i] &lt;= 10<sup>4</sup></code></li>
	<li><code>k</code> is in the range <code>[1, the number of unique elements in the array]</code>.</li>
	<li>It is <strong>guaranteed</strong> that the answer is <strong>unique</strong>.</li>
</ul>

<p>&nbsp;</p>
<p><strong>Follow up:</strong> Your algorithm&#39;s time complexity must be better than <code>O(n log n)</code>, where n is the array&#39;s size.</p>


### ZH-CN:
<p>给你一个整数数组 <code>nums</code> 和一个整数 <code>k</code> ，请你返回其中出现频率前 <code>k</code> 高的元素。你可以按 <strong>任意顺序</strong> 返回答案。</p>

<p> </p>

<p><strong>示例 1:</strong></p>

<pre>
<strong>输入: </strong>nums = [1,1,1,2,2,3], k = 2
<strong>输出: </strong>[1,2]
</pre>

<p><strong>示例 2:</strong></p>

<pre>
<strong>输入: </strong>nums = [1], k = 1
<strong>输出: </strong>[1]</pre>

<p> </p>

<p><strong>提示：</strong></p>

<ul>
	<li><code>1 <= nums.length <= 10<sup>5</sup></code></li>
	<li><code>k</code> 的取值范围是 <code>[1, 数组中不相同的元素的个数]</code></li>
	<li>题目数据保证答案唯一，换句话说，数组中前 <code>k</code> 个高频元素的集合是唯一的</li>
</ul>

<p> </p>

<p><strong>进阶：</strong>你所设计算法的时间复杂度 <strong>必须</strong> 优于 <code>O(n log n)</code> ，其中 <code>n</code><em> </em>是数组大小。</p>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/top-k-frequent-elements/description/)  -  [LeetCode-CN](https://leetcode.cn/problems/top-k-frequent-elements/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| typescript  | 92 ms | 46.4 MB | 2023/04/09 17:09 |

```typescript

function topKFrequent(nums: number[], k: number): number[] {
  const map: {
    [k: number]: number
  } = {};
  for (let i = 0; i < nums.length; i++) {
    if (map[nums[i]] !== undefined) {
      map[nums[i]] += 1;
    } else {
      map[nums[i]] = 1;
    }
  }

  const arr = Object.entries(map);
  const len = arr.length;

  const partition = (start: number, end: number) => {
    const pivotNum = arr[start];

    let i = start, j = end;

    while (i < j) {
      while (arr[j][1] >= pivotNum[1] && i < j) {
        j--;
      }

      arr[i] = arr[j];

      while (arr[i][1] < pivotNum[1] && i < j) {
        i++;
      }

      arr[j] = arr[i];
    }

    arr[i] = pivotNum;

    return i;
  }

  let i = partition(0, len - 1);

  while (i !== len - k) {
    if (i > len - k) {
      i = partition(0, i - 1);
    } else {
      i = partition(i + 1, len - 1);
    }
  }

  const ans: number[] = new Array(k).fill(-1);

  for (let i = len - k; i < len; i++) {
    ans[i - (len - k)] = Number(arr[i][0]);
  }

  return ans;
};

```
## My Notes - 我的笔记


思路：先遍历一遍，用哈希表存储每个元素的出现次数；
把这个哈希视为二元组，将、对值采用快速排序的partition进行由小到大排序，当`pivot === len - k` 时，返回后`k`个元素即可。 时间复杂度平均为 $O(n)$ ，最坏为 $O(n^2)$。
```typescript
function topKFrequent(nums: number[], k: number): number[] {
  const map: {
    [k: number]: number
  } = {};
  for (let i = 0; i < nums.length; i++) {
    if (map[nums[i]] !== undefined) {
      map[nums[i]] += 1;
    } else {
      map[nums[i]] = 1;
    }
  }

  const arr = Object.entries(map);
  const len = arr.length;

  const partition = (start: number, end: number) => {
    const pivotNum = arr[start];

    let i = start, j = end;

    while (i < j) {
      while (arr[j][1] >= pivotNum[1] && i < j) {
        j--;
      }

      arr[i] = arr[j];

      while (arr[i][1] < pivotNum[1] && i < j) {
        i++;
      }

      arr[j] = arr[i];
    }

    arr[i] = pivotNum;

    return i;
  }

  let i = partition(0, len - 1);

  while (i !== len - k) {
    if (i > len - k) {
      i = partition(0, i - 1);
    } else {
      i = partition(i + 1, len - 1);
    }
  }

  const ans: number[] = new Array(k).fill(-1);

  for (let i = len - k; i < len; i++) {
    ans[i - (len - k)] = Number(arr[i][0]);
  }

  return ans;
};
```
注意：
1. `partition` 记得取二元组的`[1]`。
2. partition 必须要等`pivot == len - k` 时才能结束，而不是`pivot < len - k`。

