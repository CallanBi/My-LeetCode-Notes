
# 85. Maximal Rectangle - 最大矩形

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Stack-栈-blue.svg">   <img src="https://img.shields.io/badge/Array-数组-blue.svg">   <img src="https://img.shields.io/badge/Dynamic Programming-动态规划-blue.svg">   <img src="https://img.shields.io/badge/Matrix-矩阵-blue.svg">   <img src="https://img.shields.io/badge/Monotonic Stack-单调栈-blue.svg">  


## Description - 题目描述

### EN:
<p>Given a <code>rows x cols</code>&nbsp;binary <code>matrix</code> filled with <code>0</code>&#39;s and <code>1</code>&#39;s, find the largest rectangle containing only <code>1</code>&#39;s and return <em>its area</em>.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2020/09/14/maximal.jpg" style="width: 402px; height: 322px;" />
<pre>
<strong>Input:</strong> matrix = [[&quot;1&quot;,&quot;0&quot;,&quot;1&quot;,&quot;0&quot;,&quot;0&quot;],[&quot;1&quot;,&quot;0&quot;,&quot;1&quot;,&quot;1&quot;,&quot;1&quot;],[&quot;1&quot;,&quot;1&quot;,&quot;1&quot;,&quot;1&quot;,&quot;1&quot;],[&quot;1&quot;,&quot;0&quot;,&quot;0&quot;,&quot;1&quot;,&quot;0&quot;]]
<strong>Output:</strong> 6
<strong>Explanation:</strong> The maximal rectangle is shown in the above picture.
</pre>

<p><strong>Example 2:</strong></p>

<pre>
<strong>Input:</strong> matrix = [[&quot;0&quot;]]
<strong>Output:</strong> 0
</pre>

<p><strong>Example 3:</strong></p>

<pre>
<strong>Input:</strong> matrix = [[&quot;1&quot;]]
<strong>Output:</strong> 1
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>rows == matrix.length</code></li>
	<li><code>cols == matrix[i].length</code></li>
	<li><code>1 &lt;= row, cols &lt;= 200</code></li>
	<li><code>matrix[i][j]</code> is <code>&#39;0&#39;</code> or <code>&#39;1&#39;</code>.</li>
</ul>


### ZH-CN:
<p>给定一个仅包含&nbsp;<code>0</code> 和 <code>1</code> 、大小为 <code>rows x cols</code> 的二维二进制矩阵，找出只包含 <code>1</code> 的最大矩形，并返回其面积。</p>

<p>&nbsp;</p>

<p><strong>示例 1：</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2020/09/14/maximal.jpg" style="width: 402px; height: 322px;" />
<pre>
<strong>输入：</strong>matrix = [["1","0","1","0","0"],["1","0","1","1","1"],["1","1","1","1","1"],["1","0","0","1","0"]]
<strong>输出：</strong>6
<strong>解释：</strong>最大矩形如上图所示。
</pre>

<p><strong>示例 2：</strong></p>

<pre>
<strong>输入：</strong>matrix = []
<strong>输出：</strong>0
</pre>

<p><strong>示例 3：</strong></p>

<pre>
<strong>输入：</strong>matrix = [["0"]]
<strong>输出：</strong>0
</pre>

<p><strong>示例 4：</strong></p>

<pre>
<strong>输入：</strong>matrix = [["1"]]
<strong>输出：</strong>1
</pre>

<p><strong>示例 5：</strong></p>

<pre>
<strong>输入：</strong>matrix = [["0","0"]]
<strong>输出：</strong>0
</pre>

<p>&nbsp;</p>

<p><strong>提示：</strong></p>

<ul>
	<li><code>rows == matrix.length</code></li>
	<li><code>cols == matrix[0].length</code></li>
	<li><code>1 &lt;= row, cols &lt;= 200</code></li>
	<li><code>matrix[i][j]</code> 为 <code>'0'</code> 或 <code>'1'</code></li>
</ul>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/maximal-rectangle/description/)  -  [LeetCode-CN](https://leetcode.cn/problems/maximal-rectangle/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| golang  | 188 ms | 7 MB | 2022/06/06 19:07 |

```golang

func maximalRectangle(matrix [][]byte) int {
  m, n := len(matrix), len(matrix[0])
  leftContinuous := make([][]int, m)
  for i := range leftContinuous {
    leftContinuous[i] = make([]int, n)
  }

  for i := 0; i < m; i++ {
    for j := 0; j < n; j++ {
      if j == 0 {
        leftContinuous[i][j], _ = strconv.Atoi(string(matrix[i][j]))
      } else {
        if matrix[i][j] == '0' {
          leftContinuous[i][j] = 0
        } else {
          leftContinuous[i][j] = leftContinuous[i][j-1] + 1
        }
      }
    }
  }

  col := make([]int, n)
  maxArea := 0

  for j := 0; j < n; j++ {
    for i := 0; i < m; i++ {
      col = append(col, leftContinuous[i][j])
      curArea := largestRectangleInArr(&col)
      if (curArea > maxArea) {
        maxArea = curArea
      }
    }
    col = make([]int, n)
  }

  return maxArea



}

func largestRectangleInArr(heights *([]int)) int {
  maxArea := 0
  leng := len(*heights)
  stack := make([]int, 0)

  for i := 0; i <= leng; i++ {
    for len(stack) > 0 && (i == leng || (*heights)[i] < (*heights)[stack[len(stack) - 1]] ) {
      curIdx := stack[len(stack) - 1]
      stack = stack[:len(stack) - 1]
      height := (*heights)[curIdx]

      var width int
      if len(stack) > 0 {
        width = i - stack[len(stack) - 1] - 1
      } else {
        width = i
      }

      curArea := width * height

      if maxArea < curArea {
        maxArea = curArea
      }
    }

    stack = append(stack, i)
  }

  return maxArea
}

```
## My Notes - 我的笔记


参考[官方题解](https://leetcode.cn/problems/maximal-rectangle/solution/zui-da-ju-xing-by-leetcode-solution-bjlu/)的单调栈法：

复用[第84题](https://leetcode.cn/problems/largest-rectangle-in-histogram/)的一维数组中的最大矩形的单调栈法。

```go
func maximalRectangle(matrix [][]byte) int {
  m, n := len(matrix), len(matrix[0])
  leftContinuous := make([][]int, m)
  for i := range leftContinuous {
    leftContinuous[i] = make([]int, n)
  }

  for i := 0; i < m; i++ {
    for j := 0; j < n; j++ {
      if j == 0 {
        leftContinuous[i][j], _ = strconv.Atoi(string(matrix[i][j]))
      } else {
        if matrix[i][j] == '0' {
          leftContinuous[i][j] = 0
        } else {
          leftContinuous[i][j] = leftContinuous[i][j-1] + 1
        }
      }
    }
  }

  col := make([]int, n)
  maxArea := 0

  for j := 0; j < n; j++ {
    for i := 0; i < m; i++ {
      col = append(col, leftContinuous[i][j])
      curArea := largestRectangleInArr(&col)
      if (curArea > maxArea) {
        maxArea = curArea
      }
    }
    col = make([]int, n)
  }

  return maxArea



}

func largestRectangleInArr(heights *([]int)) int {
  maxArea := 0
  leng := len(*heights)
  stack := make([]int, 0)

  for i := 0; i <= leng; i++ {
    for len(stack) > 0 && (i == leng || (*heights)[i] < (*heights)[stack[len(stack) - 1]] ) {
      curIdx := stack[len(stack) - 1]
      stack = stack[:len(stack) - 1]
      height := (*heights)[curIdx]

      var width int
      if len(stack) > 0 {
        width = i - stack[len(stack) - 1] - 1
      } else {
        width = i
      }

      curArea := width * height

      if maxArea < curArea {
        maxArea = curArea
      }
    }

    stack = append(stack, i)
  }

  return maxArea
}
```


