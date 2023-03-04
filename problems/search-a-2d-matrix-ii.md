
# 240. Search a 2D Matrix II - 搜索二维矩阵 II

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Array-数组-blue.svg">   <img src="https://img.shields.io/badge/Binary Search-二分查找-blue.svg">   <img src="https://img.shields.io/badge/Divide and Conquer-分治-blue.svg">   <img src="https://img.shields.io/badge/Matrix-矩阵-blue.svg">  


## Description - 题目描述

### EN:
<p>Write an efficient algorithm that searches for a value <code>target</code> in an <code>m x n</code> integer matrix <code>matrix</code>. This matrix has the following properties:</p>

<ul>
	<li>Integers in each row are sorted in ascending from left to right.</li>
	<li>Integers in each column are sorted in ascending from top to bottom.</li>
</ul>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2020/11/24/searchgrid2.jpg" style="width: 300px; height: 300px;" />
<pre>
<strong>Input:</strong> matrix = [[1,4,7,11,15],[2,5,8,12,19],[3,6,9,16,22],[10,13,14,17,24],[18,21,23,26,30]], target = 5
<strong>Output:</strong> true
</pre>

<p><strong class="example">Example 2:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2020/11/24/searchgrid.jpg" style="width: 300px; height: 300px;" />
<pre>
<strong>Input:</strong> matrix = [[1,4,7,11,15],[2,5,8,12,19],[3,6,9,16,22],[10,13,14,17,24],[18,21,23,26,30]], target = 20
<strong>Output:</strong> false
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>m == matrix.length</code></li>
	<li><code>n == matrix[i].length</code></li>
	<li><code>1 &lt;= n, m &lt;= 300</code></li>
	<li><code>-10<sup>9</sup> &lt;= matrix[i][j] &lt;= 10<sup>9</sup></code></li>
	<li>All the integers in each row are <strong>sorted</strong> in ascending order.</li>
	<li>All the integers in each column are <strong>sorted</strong> in ascending order.</li>
	<li><code>-10<sup>9</sup> &lt;= target &lt;= 10<sup>9</sup></code></li>
</ul>


### ZH-CN:
<p>编写一个高效的算法来搜索&nbsp;<code><em>m</em>&nbsp;x&nbsp;<em>n</em></code>&nbsp;矩阵 <code>matrix</code> 中的一个目标值 <code>target</code> 。该矩阵具有以下特性：</p>

<ul>
	<li>每行的元素从左到右升序排列。</li>
	<li>每列的元素从上到下升序排列。</li>
</ul>

<p>&nbsp;</p>

<p><b>示例 1：</b></p>
<img alt="" src="https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2020/11/25/searchgrid2.jpg" />
<pre>
<b>输入：</b>matrix = [[1,4,7,11,15],[2,5,8,12,19],[3,6,9,16,22],[10,13,14,17,24],[18,21,23,26,30]], target = 5
<b>输出：</b>true
</pre>

<p><b>示例 2：</b></p>
<img alt="" src="https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2020/11/25/searchgrid.jpg" />
<pre>
<b>输入：</b>matrix = [[1,4,7,11,15],[2,5,8,12,19],[3,6,9,16,22],[10,13,14,17,24],[18,21,23,26,30]], target = 20
<b>输出：</b>false
</pre>

<p>&nbsp;</p>

<p><strong>提示：</strong></p>

<ul>
	<li><code>m == matrix.length</code></li>
	<li><code>n == matrix[i].length</code></li>
	<li><code>1 &lt;= n, m &lt;= 300</code></li>
	<li><code>-10<sup>9</sup>&nbsp;&lt;= matrix[i][j] &lt;= 10<sup>9</sup></code></li>
	<li>每行的所有元素从左到右升序排列</li>
	<li>每列的所有元素从上到下升序排列</li>
	<li><code>-10<sup>9</sup>&nbsp;&lt;= target &lt;= 10<sup>9</sup></code></li>
</ul>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/search-a-2d-matrix-ii/description/)  -  [LeetCode-CN](https://leetcode.cn/problems/search-a-2d-matrix-ii/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| typescript  | 84 ms | 41 MB | 2021/04/03 19:20 |

```typescript

function searchMatrix(matrix: number[][], target: number): boolean {
  // if(!matrix || !matrix[0]) {
  //   return false;
  // }
  // const rightCornor = matrix[0][matrix[0].length-1];
  // // console.log(rightCornor)
  // if (!rightCornor && typeof rightCornor !== 'number') {
  //   return false;
  // }
  // if (target < rightCornor) {
  //   const newMatrix = matrix.map(row => {
  //     const newRow = [...row];
  //     newRow.splice(row.length-1, 1);
  //     return newRow;
  //   });
  //   // console.log(newMatrix)

  //   return searchMatrix(newMatrix, target);
  // } else if (target > rightCornor) {
  //   const newMatrix = [...matrix];
  //   newMatrix.splice(0,1);
  //   // console.log(newMatrix)

  //   return searchMatrix(newMatrix, target);
  // } else {
  //   // 相等
  //   return true;
  // }
  return matrix.findIndex(row => row.findIndex(ele => ele === target) !== -1 ? true : false ) !== -1 ? true : false;
};

```
## My Notes - 我的笔记


用剑指 offer 提供的思路实现，开销较大
```typescript
function searchMatrix(matrix: number[][], target: number): boolean {
  if(!matrix || !matrix[0]) {
    return false;
  }
  const rightCornor = matrix[0][matrix[0].length-1];
  // console.log(rightCornor)
  if (!rightCornor && typeof rightCornor !== 'number') {
    return false;
  }
  if (target < rightCornor) {
    const newMatrix = matrix.map(row => {
      const newRow = [...row];
      newRow.splice(row.length-1, 1);
      return newRow;
    });
    // console.log(newMatrix)

    return searchMatrix(newMatrix, target);
  } else if (target > rightCornor) {
    const newMatrix = [...matrix];
    newMatrix.splice(0,1);
    // console.log(newMatrix)

    return searchMatrix(newMatrix, target);
  } else {
    // 相等
    return true;
  }
};
```

直接一行代码暴力解决吧
```typescript
return matrix.findIndex(row => row.findIndex(ele => ele === target) !== -1 ? true : false ) !== -1 ? true : false;
```

