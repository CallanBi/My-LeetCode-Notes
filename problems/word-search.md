
# 79. Word Search - 单词搜索

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Array-数组-blue.svg">   <img src="https://img.shields.io/badge/Backtracking-回溯-blue.svg">   <img src="https://img.shields.io/badge/Matrix-矩阵-blue.svg">  


## Description - 题目描述

### EN:
<p>Given an <code>m x n</code> grid of characters <code>board</code> and a string <code>word</code>, return <code>true</code> <em>if</em> <code>word</code> <em>exists in the grid</em>.</p>

<p>The word can be constructed from letters of sequentially adjacent cells, where adjacent cells are horizontally or vertically neighboring. The same letter cell may not be used more than once.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2020/11/04/word2.jpg" style="width: 322px; height: 242px;" />
<pre>
<strong>Input:</strong> board = [[&quot;A&quot;,&quot;B&quot;,&quot;C&quot;,&quot;E&quot;],[&quot;S&quot;,&quot;F&quot;,&quot;C&quot;,&quot;S&quot;],[&quot;A&quot;,&quot;D&quot;,&quot;E&quot;,&quot;E&quot;]], word = &quot;ABCCED&quot;
<strong>Output:</strong> true
</pre>

<p><strong>Example 2:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2020/11/04/word-1.jpg" style="width: 322px; height: 242px;" />
<pre>
<strong>Input:</strong> board = [[&quot;A&quot;,&quot;B&quot;,&quot;C&quot;,&quot;E&quot;],[&quot;S&quot;,&quot;F&quot;,&quot;C&quot;,&quot;S&quot;],[&quot;A&quot;,&quot;D&quot;,&quot;E&quot;,&quot;E&quot;]], word = &quot;SEE&quot;
<strong>Output:</strong> true
</pre>

<p><strong>Example 3:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2020/10/15/word3.jpg" style="width: 322px; height: 242px;" />
<pre>
<strong>Input:</strong> board = [[&quot;A&quot;,&quot;B&quot;,&quot;C&quot;,&quot;E&quot;],[&quot;S&quot;,&quot;F&quot;,&quot;C&quot;,&quot;S&quot;],[&quot;A&quot;,&quot;D&quot;,&quot;E&quot;,&quot;E&quot;]], word = &quot;ABCB&quot;
<strong>Output:</strong> false
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>m == board.length</code></li>
	<li><code>n = board[i].length</code></li>
	<li><code>1 &lt;= m, n &lt;= 6</code></li>
	<li><code>1 &lt;= word.length &lt;= 15</code></li>
	<li><code>board</code> and <code>word</code> consists of only lowercase and uppercase English letters.</li>
</ul>

<p>&nbsp;</p>
<p><strong>Follow up:</strong> Could you use search pruning to make your solution faster with a larger <code>board</code>?</p>


### ZH-CN:
<p>给定一个 <code>m x n</code> 二维字符网格 <code>board</code> 和一个字符串单词 <code>word</code> 。如果 <code>word</code> 存在于网格中，返回 <code>true</code> ；否则，返回 <code>false</code> 。</p>

<p>单词必须按照字母顺序，通过相邻的单元格内的字母构成，其中“相邻”单元格是那些水平相邻或垂直相邻的单元格。同一个单元格内的字母不允许被重复使用。</p>

<p> </p>

<p><strong>示例 1：</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2020/11/04/word2.jpg" style="width: 322px; height: 242px;" />
<pre>
<strong>输入：</strong>board = [["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]], word = "ABCCED"
<strong>输出：</strong>true
</pre>

<p><strong>示例 2：</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2020/11/04/word-1.jpg" style="width: 322px; height: 242px;" />
<pre>
<strong>输入：</strong>board = [["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]], word = "SEE"
<strong>输出：</strong>true
</pre>

<p><strong>示例 3：</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2020/10/15/word3.jpg" style="width: 322px; height: 242px;" />
<pre>
<strong>输入：</strong>board = [["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]], word = "ABCB"
<strong>输出：</strong>false
</pre>

<p> </p>

<p><strong>提示：</strong></p>

<ul>
	<li><code>m == board.length</code></li>
	<li><code>n = board[i].length</code></li>
	<li><code>1 <= m, n <= 6</code></li>
	<li><code>1 <= word.length <= 15</code></li>
	<li><code>board</code> 和 <code>word</code> 仅由大小写英文字母组成</li>
</ul>

<p> </p>

<p><strong>进阶：</strong>你可以使用搜索剪枝的技术来优化解决方案，使其在 <code>board</code> 更大的情况下可以更快解决问题？</p>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/word-search/description/)  -  [LeetCode-CN](https://leetcode.cn/problems/word-search/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| typescript  | 276 ms | 42.7 MB | 2022/06/02 15:08 |

```typescript

function exist(board: string[][], word: string): boolean {

  const m = board.length;

  const n = board[0].length;

  const isUsed: boolean[][] = new Array(m).fill(false).map(_ => new Array(n).fill(false));


  function backtrack(row: number, col: number, wordIdx: number): boolean {
    if (row >= m || row < 0) {
      return false;
    }
    if (col >= n || col < 0) {
      return false;
    }

    if (isUsed[row][col]) {
      return false;
    }

    if (wordIdx >= word.length) {
      return true;
    }

    if (board[row][col] === word[wordIdx]) {
      if (wordIdx === word.length - 1) {
        isUsed[row][col] = false;
        return true;
      }
      isUsed[row][col] = true;
      const res = backtrack(row + 1, col, wordIdx + 1) || backtrack(row, col + 1, wordIdx + 1) || backtrack(row - 1, col, wordIdx + 1) || backtrack(row, col - 1, wordIdx + 1);
      isUsed[row][col] = false;
      return res;
    } else {
      isUsed[row][col] = false;
      return false;
    }
  }

  for (let i = 0; i < m; i++) {
    for (let j = 0; j < n; j++) {
      const res = backtrack(i, j, 0);
      if (res) {
        return true;
      }
    }
  }

  return false;
};

```
## My Notes - 我的笔记


本题与 剑指 Offer 12. 矩阵中的路径 LCOF 相同，可参考[那边的题解](https://github.com/CallanBi/My-LeetCode-Notes/blob/master/problems/ju-zhen-zhong-de-lu-jing-lcof.md)。

但我感觉这次 AC 的写法更好看，代码简洁性能好。

```typescript
function exist(board: string[][], word: string): boolean {

  const m = board.length;

  const n = board[0].length;

  const isUsed: boolean[][] = new Array(m).fill(false).map(_ => new Array(n).fill(false));


  function backtrack(row: number, col: number, wordIdx: number): boolean {
    if (row >= m || row < 0) {
      return false;
    }
    if (col >= n || col < 0) {
      return false;
    }

    if (isUsed[row][col]) {
      return false;
    }

    if (wordIdx >= word.length) {
      return true;
    }

    if (board[row][col] === word[wordIdx]) {
      if (wordIdx === word.length - 1) {
        isUsed[row][col] = false;
        return true;
      }
      isUsed[row][col] = true;
      const res = backtrack(row + 1, col, wordIdx + 1) || backtrack(row, col + 1, wordIdx + 1) || backtrack(row - 1, col, wordIdx + 1) || backtrack(row, col - 1, wordIdx + 1);
      isUsed[row][col] = false;
      return res;
    } else {
      isUsed[row][col] = false;
      return false;
    }
  }

  for (let i = 0; i < m; i++) {
    for (let j = 0; j < n; j++) {
      const res = backtrack(i, j, 0);
      if (res) {
        return true;
      }
    }
  }

  return false;
};
```


