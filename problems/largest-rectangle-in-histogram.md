
# 84. Largest Rectangle in Histogram - 柱状图中最大的矩形

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Stack-栈-blue.svg">   <img src="https://img.shields.io/badge/Array-数组-blue.svg">   <img src="https://img.shields.io/badge/Monotonic Stack-单调栈-blue.svg">  


## Description - 题目描述

### EN:
<p>Given an array of integers <code>heights</code> representing the histogram&#39;s bar height where the width of each bar is <code>1</code>, return <em>the area of the largest rectangle in the histogram</em>.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2021/01/04/histogram.jpg" style="width: 522px; height: 242px;" />
<pre>
<strong>Input:</strong> heights = [2,1,5,6,2,3]
<strong>Output:</strong> 10
<strong>Explanation:</strong> The above is a histogram where width of each bar is 1.
The largest rectangle is shown in the red area, which has an area = 10 units.
</pre>

<p><strong>Example 2:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2021/01/04/histogram-1.jpg" style="width: 202px; height: 362px;" />
<pre>
<strong>Input:</strong> heights = [2,4]
<strong>Output:</strong> 4
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= heights.length &lt;= 10<sup>5</sup></code></li>
	<li><code>0 &lt;= heights[i] &lt;= 10<sup>4</sup></code></li>
</ul>


### ZH-CN:
<p>给定 <em>n</em> 个非负整数，用来表示柱状图中各个柱子的高度。每个柱子彼此相邻，且宽度为 1 。</p>

<p>求在该柱状图中，能够勾勒出来的矩形的最大面积。</p>

<p> </p>

<p><strong>示例 1:</strong></p>

<p><img src="https://assets.leetcode.com/uploads/2021/01/04/histogram.jpg" /></p>

<pre>
<strong>输入：</strong>heights = [2,1,5,6,2,3]
<strong>输出：</strong>10
<strong>解释：</strong>最大的矩形为图中红色区域，面积为 10
</pre>

<p><strong>示例 2：</strong></p>

<p><img src="https://assets.leetcode.com/uploads/2021/01/04/histogram-1.jpg" /></p>

<pre>
<strong>输入：</strong> heights = [2,4]
<b>输出：</b> 4</pre>

<p> </p>

<p><strong>提示：</strong></p>

<ul>
	<li><code>1 <= heights.length <=10<sup>5</sup></code></li>
	<li><code>0 <= heights[i] <= 10<sup>4</sup></code></li>
</ul>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/largest-rectangle-in-histogram/description/)  -  [LeetCode-CN](https://leetcode.cn/problems/largest-rectangle-in-histogram/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| typescript  | 84 ms | 52.7 MB | 2022/06/02 19:31 |

```typescript

function largestRectangleArea(heights: number[]): number {
  let i = 0,
    maxArea = 0,
    stack = [];

  for (let i = 0, len = heights.length; i <= len; i++) {
    while (stack.length > 0 && (heights[i] < heights[stack[stack.length - 1]] || i === len)) {
      const curIdx = stack.pop();
      const height = heights[curIdx],
        width = stack.length > 0 ? i - stack[stack.length - 1] - 1 : i;

      maxArea = Math.max(maxArea, width * height);
    }

    stack.push(i);
  }

  return maxArea;
};

```
## My Notes - 我的笔记


单调栈法，思路：[JavaScript版解题思路](https://leetcode.cn/problems/largest-rectangle-in-histogram/solution/javascriptban-jie-ti-si-lu-by-ityou-o-znkf/)

这个思路的合理之处在于：对于单调递增栈内的每一个元素，位于它的栈顶方向的元素总是比它要大。

这时，以它为高的矩形，所延伸出的最大面积，便是一直往栈顶方向延伸的面积。

比如，我们考虑 `[2,1,5,6,2,3]`这个例子。

当我们遍历到索引为`4`，即遍历到高度为`2`的这个柱子时，栈的内容是 `[1,2,3]`，对应的高度是 `[1,5,6]`。

对于栈中高度为 `[1,5,6]`的这几个柱子的每一个元素，其可以向右延伸的最大宽度是从它左边比他小的柱子的索引到当前遍历元素所在索引之间的距离。

比如对于高度为$6$的柱子，其可以延伸的宽度为 $4 - 2 - 1$，`4`即为当前遍历的元素，`2` 即为栈中前一个栈底方向的元素，这两个元素构成了最大宽度的边界。真正的距离是一个开区间：$x \in (2,4) \ and \ x \in N$ 的连续部分。

同理，对于高度为$5$的柱子，其可以延伸的宽度为 $4 - 1 - 1$。

特殊情况是单调栈遍历到最后一个元素，这时它已经没有栈底方向的元素了。这时候，它延伸的距离是**从 `0`开始到 当前遍历元素的距离**。

如这个例子中，当我们出栈到高度为$1$的柱子时，栈已经空了，但由于单调栈的性质，我们可以知道比$1$这个柱子高的柱子肯定都已经先于$1$出栈了。所以先于$1$出栈的柱子都比它大，故`heights`中索引比$1$这个柱子小的柱子肯定都是大过它的。因此，它向左边的延伸方向可以到索引为`0`的柱子下。

故我们可以写出这样的代码：

```typescript
function largestRectangleArea(heights: number[]): number {
  let i = 0,
    maxArea = 0,
    stack = [];

  for (let i = 0, len = heights.length; i <= len; i++) {
    while (stack.length > 0 && (heights[i] < heights[stack[stack.length - 1]] || i === len)) {
      const curIdx = stack.pop();
      const height = heights[curIdx],
        width = stack.length > 0 ? i - stack[stack.length - 1] - 1 : i;

      maxArea = Math.max(maxArea, width * height);
    }

    stack.push(i);
  }

  return maxArea;
};
```


