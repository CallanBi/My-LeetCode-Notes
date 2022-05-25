
# 剑指 Offer 12. 矩阵中的路径  LCOF - 矩阵中的路径

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Array-数组-blue.svg">   <img src="https://img.shields.io/badge/Backtracking-回溯-blue.svg">   <img src="https://img.shields.io/badge/Matrix-矩阵-blue.svg">  


## Description - 题目描述

### EN:
English description is not available for the problem. Please switch to Chinese.

### ZH-CN:
<p>给定一个 <code>m x n</code> 二维字符网格 <code>board</code> 和一个字符串单词 <code>word</code> 。如果 <code>word</code> 存在于网格中，返回 <code>true</code> ；否则，返回 <code>false</code> 。</p>

<p>单词必须按照字母顺序，通过相邻的单元格内的字母构成，其中“相邻”单元格是那些水平相邻或垂直相邻的单元格。同一个单元格内的字母不允许被重复使用。</p>

<p> </p>

<p>例如，在下面的 3×4 的矩阵中包含单词 "ABCCED"（单词中的字母已标出）。</p>

<p><img alt="" src="https://assets.leetcode.com/uploads/2020/11/04/word2.jpg" style="width: 322px; height: 242px;" /></p>

<p> </p>

<p><strong>示例 1：</strong></p>

<pre>
<strong>输入：</strong>board = [["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]], word = "ABCCED"
<strong>输出：</strong>true
</pre>

<p><strong>示例 2：</strong></p>

<pre>
<strong>输入：</strong>board = [["a","b"],["c","d"]], word = "abcd"
<strong>输出：</strong>false
</pre>

<p> </p>

<p><strong>提示：</strong></p>

<ul>
	<li><code>1 <= board.length <= 200</code></li>
	<li><code>1 <= board[i].length <= 200</code></li>
	<li><code>board</code> 和 <code>word</code> 仅由大小写英文字母组成</li>
</ul>

<p> </p>

<p><strong>注意：</strong>本题与主站 79 题相同：<a href="https://leetcode-cn.com/problems/word-search/">https://leetcode-cn.com/problems/word-search/</a></p>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/ju-zhen-zhong-de-lu-jing-lcof/description/)  -  [LeetCode-CN](https://leetcode.cn/problems/ju-zhen-zhong-de-lu-jing-lcof/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| typescript  | 2288 ms | 47.8 MB | 2021/04/08 2:53 |

```typescript

/**
 * 回溯法查找单个字母是否有路径
 */
const singleLetterHasPath = (board: string[][], isUsed: boolean[][], word: string, x: number, y: number) => {
  if (!word || word.length === 0) {
    return true;
  }
  if (!board[y]) {
    return false;
  }
  if (!board[y][x]) {
    return false;
  }
  
  if (isUsed[y][x]) {
    return false;
  }

  isUsed[y][x] = true;

  const res = 
    board[y][x] === word[0] 
    && (singleLetterHasPath(board, isUsed, word.slice(1), x, y-1) 
    || singleLetterHasPath(board, isUsed, word.slice(1), x, y+1) 
    || singleLetterHasPath(board, isUsed, word.slice(1), x-1, y) 
    || singleLetterHasPath(board, isUsed, word.slice(1), x+1, y));

  if (!res) {
    isUsed[y][x] = false;
  }
  return res;
}

function exist(board: string[][], word: string): boolean {
  if (!board) {
    return false;
  }
  if (board.length === 0) {
    return false;
  }
  if (!word) {
    return true;
  }

  return board.some((row, rowIdx) => row.some((col, colIdx) => 
    singleLetterHasPath(
      board,
      new Array<boolean[]>(board.length).fill([]).map(i => new Array<boolean>(board[0].length).fill(false)),
      word,
      colIdx,
      rowIdx
    )
  ));
};

```
## My Notes - 我的笔记


典型回溯法题目。

回溯法可参考：[回溯法 - OI Wiki](https://oi-wiki.org/search/backtracking/)

回溯法本质上是 DFS，但多了一个边界条件（比如这道题的 `isUsed`）。碰到边界条件就不再搜索，转而搜索另一条链。

```typescript
/**
 * 回溯法查找单个字母是否有路径
 */
const singleLetterHasPath = (board: string[][], isUsed: boolean[][], word: string, x: number, y: number) => {
  if (!word || word.length === 0) {
    return true;
  }
  if (!board[y]) {
    return false;
  }
  if (!board[y][x]) {
    return false;
  }
  
  if (isUsed[y][x]) {
    return false;
  }

  isUsed[y][x] = true;

  const res = 
    board[y][x] === word[0] 
    && (singleLetterHasPath(board, isUsed, word.slice(1), x, y-1) 
    || singleLetterHasPath(board, isUsed, word.slice(1), x, y+1) 
    || singleLetterHasPath(board, isUsed, word.slice(1), x-1, y) 
    || singleLetterHasPath(board, isUsed, word.slice(1), x+1, y));

  if (!res) {
    isUsed[y][x] = false;
  }
  return res;
}

function exist(board: string[][], word: string): boolean {
  if (!board) {
    return false;
  }
  if (board.length === 0) {
    return false;
  }
  if (!word) {
    return true;
  }

  return board.some((row, rowIdx) => row.some((col, colIdx) => 
    singleLetterHasPath(
      board,
      new Array<boolean[]>(board.length).fill([]).map(i => new Array<boolean>(board[0].length).fill(false)),
      word,
      colIdx,
      rowIdx
    )
  ));
};
```

## 坑点：

创建指定空间大小的二维数组，不能这样写：

```typescript
new Array<boolean[]>(board.length).fill(new Array<boolean>(board[0].length).fill(false)),
```

`new Array`只被创建了一次。实际上二维数组引用的行是同一个。当设置 `a[0][0] === true`时，所有行的第一个元素都被设置为` true`，不符合预期。


