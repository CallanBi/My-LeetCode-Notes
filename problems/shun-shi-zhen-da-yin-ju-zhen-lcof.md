
# 剑指 Offer 29. 顺时针打印矩阵  LCOF - 顺时针打印矩阵

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Array-数组-blue.svg">   <img src="https://img.shields.io/badge/Matrix-矩阵-blue.svg">   <img src="https://img.shields.io/badge/Simulation-模拟-blue.svg">  


## Description - 题目描述

### EN:
English description is not available for the problem. Please switch to Chinese.

### ZH-CN:
<p>输入一个矩阵，按照从外向里以顺时针的顺序依次打印出每一个数字。</p>

<p>&nbsp;</p>

<p><strong>示例 1：</strong></p>

<pre><strong>输入：</strong>matrix = [[1,2,3],[4,5,6],[7,8,9]]
<strong>输出：</strong>[1,2,3,6,9,8,7,4,5]
</pre>

<p><strong>示例 2：</strong></p>

<pre><strong>输入：</strong>matrix =&nbsp;[[1,2,3,4],[5,6,7,8],[9,10,11,12]]
<strong>输出：</strong>[1,2,3,4,8,12,11,10,9,5,6,7]
</pre>

<p>&nbsp;</p>

<p><strong>限制：</strong></p>

<ul>
	<li><code>0 &lt;= matrix.length &lt;= 100</code></li>
	<li><code>0 &lt;= matrix[i].length&nbsp;&lt;= 100</code></li>
</ul>

<p>注意：本题与主站 54 题相同：<a href="https://leetcode-cn.com/problems/spiral-matrix/">https://leetcode-cn.com/problems/spiral-matrix/</a></p>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/shun-shi-zhen-da-yin-ju-zhen-lcof/description/)  -  [LeetCode-CN](https://leetcode-cn.com/problems/shun-shi-zhen-da-yin-ju-zhen-lcof/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| typescript  | 100 ms | 42.4 MB | 2021/11/07 17:13 |

```typescript

function spiralOrder(matrix: number[][]): number[] {
  const res: number[] = [];
  if (matrix.length === 0) {
    // 排除 matrix === [] 的形态
    return [];
  }
  let horizontal = matrix[0].length, vertical = matrix.length; // 动态边界
  if (horizontal === 0 || vertical === 0) {
    return [];
  }
  let x = 0, y = 0; // x, y 标出当前位置
  while (horizontal > 0 && vertical > 0) {
    for (let i = 0; i < horizontal; i++) {
      res.push(matrix[x][y]);
      y++;
    }
    y--; // 回正位置
    vertical--; // 动态边界变小
    x++; // 移动到下一个位置
    if (horizontal === 0 || vertical === 0) {
      // 当动态边界为0时随时 break
      break;
    }
    for (let j = 0; j < vertical; j++) {
      res.push(matrix[x][y]);
      x++;
    }
    x--;
    horizontal--;
    y--;
    if (horizontal === 0 || vertical === 0) {
      break;
    }
    for (let i = horizontal; i > 0; i--) {
      res.push(matrix[x][y]);
      y--;
    }
    y++;
    vertical--;
    x--;
    if (horizontal === 0 || vertical === 0) {
      break;
    }
    for (let j = vertical; j > 0; j--) {
      res.push(matrix[x][y]);
      x--;
    }
    x++;
    horizontal--;
    y++;
    if (horizontal === 0 || vertical === 0) {
      break;
    }
  }
  return res;
};

```
## My Notes - 我的笔记


# 第一遍写时自己的代码：
```typescript
function spiralOrder(matrix: number[][]): number[] {
  const res: number[] = [];
  if (matrix.length === 0) {
    // 排除 matrix === [] 的形态
    return [];
  }
  let horizontal = matrix[0].length, vertical = matrix.length; // 动态边界
  if (horizontal === 0 || vertical === 0) {
    return [];
  }
  let x = 0, y = 0; // x, y 标出当前位置
  while (horizontal > 0 && vertical > 0) {
    for (let i = 0; i < horizontal; i++) {
      res.push(matrix[x][y]);
      y++;
    }
    y--; // 回正位置
    vertical--; // 动态边界变小
    x++; // 移动到下一个位置
    if (horizontal === 0 || vertical === 0) {
      // 当动态边界为0时随时 break
      break;
    }
    for (let j = 0; j < vertical; j++) {
      res.push(matrix[x][y]);
      x++;
    }
    x--;
    horizontal--;
    y--;
    if (horizontal === 0 || vertical === 0) {
      break;
    }
    for (let i = horizontal; i > 0; i--) {
      res.push(matrix[x][y]);
      y--;
    }
    y++;
    vertical--;
    x--;
    if (horizontal === 0 || vertical === 0) {
      break;
    }
    for (let j = vertical; j > 0; j--) {
      res.push(matrix[x][y]);
      x--;
    }
    x++;
    horizontal--;
    y++;
    if (horizontal === 0 || vertical === 0) {
      break;
    }
  }
  return res;
};
```

