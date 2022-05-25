
# 剑指 Offer 04. 二维数组中的查找 LCOF - 二维数组中的查找

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Array-数组-blue.svg">   <img src="https://img.shields.io/badge/Binary Search-二分查找-blue.svg">   <img src="https://img.shields.io/badge/Divide and Conquer-分治-blue.svg">   <img src="https://img.shields.io/badge/Matrix-矩阵-blue.svg">  


## Description - 题目描述

### EN:
<p>English description is not available for the problem. Please switch to Chinese.</p>


### ZH-CN:
<p>在一个 n * m 的二维数组中，每一行都按照从左到右递增的顺序排序，每一列都按照从上到下递增的顺序排序。请完成一个高效的函数，输入这样的一个二维数组和一个整数，判断数组中是否含有该整数。</p>

<p> </p>

<p><strong>示例:</strong></p>

<p>现有矩阵 matrix 如下：</p>

<pre>
[
  [1,   4,  7, 11, 15],
  [2,   5,  8, 12, 19],
  [3,   6,  9, 16, 22],
  [10, 13, 14, 17, 24],
  [18, 21, 23, 26, 30]
]
</pre>

<p>给定 target = <code>5</code>，返回 <code>true</code>。</p>

<p>给定 target = <code>20</code>，返回 <code>false</code>。</p>

<p> </p>

<p><strong>限制：</strong></p>

<p><code>0 <= n <= 1000</code></p>

<p><code>0 <= m <= 1000</code></p>

<p> </p>

<p><strong>注意：</strong>本题与主站 240 题相同：<a href="https://leetcode-cn.com/problems/search-a-2d-matrix-ii/">https://leetcode-cn.com/problems/search-a-2d-matrix-ii/</a></p>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/er-wei-shu-zu-zhong-de-cha-zhao-lcof/description/)  -  [LeetCode-CN](https://leetcode.cn/problems/er-wei-shu-zu-zhong-de-cha-zhao-lcof/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| typescript  | 100 ms | 40.9 MB | 2021/04/03 19:32 |

```typescript

function findNumberIn2DArray(matrix: number[][], target: number): boolean {
  // if(!matrix || !matrix[0]) {
  //     return false;
  //   }
  //   const rightCornor = matrix[0][matrix[0].length-1];
  //   // console.log(rightCornor)
  //   if (!rightCornor && typeof rightCornor !== 'number') {
  //     return false;
  //   }
  //   if (target < rightCornor) {
  //     const newMatrix = matrix.map(row => {
  //       const newRow = [...row];
  //       newRow.splice(row.length-1, 1);
  //       return newRow;
  //     });
  //     // console.log(newMatrix)

  //     return findNumberIn2DArray(newMatrix, target);
  //   } else if (target > rightCornor) {
  //     const newMatrix = [...matrix];
  //     newMatrix.splice(0,1);
  //     // console.log(newMatrix)

  //     return findNumberIn2DArray(newMatrix, target);
  //   } else {
  //     // 相等
  //     return true;
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

```
return matrix.findIndex(row => row.findIndex(ele => ele === target) !== -1 ? true : false ) !== -1 ? true : false;
```

