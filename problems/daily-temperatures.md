
# 739. Daily Temperatures - 每日温度

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Stack-栈-blue.svg">   <img src="https://img.shields.io/badge/Array-数组-blue.svg">   <img src="https://img.shields.io/badge/Monotonic Stack-单调栈-blue.svg">  


## Description - 题目描述

### EN:
<p>Given an array of integers <code>temperatures</code> represents the daily temperatures, return <em>an array</em> <code>answer</code> <em>such that</em> <code>answer[i]</code> <em>is the number of days you have to wait after the</em> <code>i<sup>th</sup></code> <em>day to get a warmer temperature</em>. If there is no future day for which this is possible, keep <code>answer[i] == 0</code> instead.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>
<pre><strong>Input:</strong> temperatures = [73,74,75,71,69,72,76,73]
<strong>Output:</strong> [1,1,4,2,1,1,0,0]
</pre><p><strong class="example">Example 2:</strong></p>
<pre><strong>Input:</strong> temperatures = [30,40,50,60]
<strong>Output:</strong> [1,1,1,0]
</pre><p><strong class="example">Example 3:</strong></p>
<pre><strong>Input:</strong> temperatures = [30,60,90]
<strong>Output:</strong> [1,1,0]
</pre>
<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;=&nbsp;temperatures.length &lt;= 10<sup>5</sup></code></li>
	<li><code>30 &lt;=&nbsp;temperatures[i] &lt;= 100</code></li>
</ul>


### ZH-CN:
<p>给定一个整数数组&nbsp;<code>temperatures</code>&nbsp;，表示每天的温度，返回一个数组&nbsp;<code>answer</code>&nbsp;，其中&nbsp;<code>answer[i]</code>&nbsp;是指对于第 <code>i</code> 天，下一个更高温度出现在几天后。如果气温在这之后都不会升高，请在该位置用&nbsp;<code>0</code> 来代替。</p>

<p>&nbsp;</p>

<p><strong>示例 1:</strong></p>

<pre>
<strong>输入:</strong> <code>temperatures</code> = [73,74,75,71,69,72,76,73]
<strong>输出:</strong>&nbsp;[1,1,4,2,1,1,0,0]
</pre>

<p><strong>示例 2:</strong></p>

<pre>
<strong>输入:</strong> temperatures = [30,40,50,60]
<strong>输出:</strong>&nbsp;[1,1,1,0]
</pre>

<p><strong>示例 3:</strong></p>

<pre>
<strong>输入:</strong> temperatures = [30,60,90]
<strong>输出: </strong>[1,1,0]</pre>

<p>&nbsp;</p>

<p><strong>提示：</strong></p>

<ul>
	<li><code>1 &lt;=&nbsp;temperatures.length &lt;= 10<sup>5</sup></code></li>
	<li><code>30 &lt;=&nbsp;temperatures[i]&nbsp;&lt;= 100</code></li>
</ul>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/daily-temperatures/description/)  -  [LeetCode-CN](https://leetcode.cn/problems/daily-temperatures/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| typescript  | 252 ms | 62.8 MB | 2023/08/12 23:12 |

```typescript

function dailyTemperatures(temperatures: number[]): number[] {
  const ans = new Array(temperatures.length).fill(0);

  const stack: number[] = [];


  for (let i = 0; i < temperatures.length; i++) {
    // console.log(stack);
    // console.log(i);
    while (temperatures.length > 0 && temperatures[stack[stack.length - 1]] < temperatures[i]) {
      const s = stack.pop();
      ans[s] = i - s;
    }
    stack.push(i);
  }

  return ans;
};

```
## My Notes - 我的笔记


# 单调栈
判别是否需要使用单调栈，如果需要找到左边或者右边第一个比当前位置的数大或者小，则可以考虑使用单调栈；单调栈的题目如矩形面积等等

单调栈有两个循环，第一个是遍历数组，第二个是while循环做出栈操作。但不能认为有两个循环，时间复杂度就是 $O(n^2)$ 。实际上单调栈算法的时间复杂度是$O(n)$。

ChatGPT4 的回答：
> 这是一个很好的问题。在这个问题中，我们用到了一个叫做"单调栈"的数据结构。这个栈的特性是，它始终保持一个单调递减的顺序。当我们遇到一个比栈顶元素大的元素时，我们就弹出栈顶元素，直到栈顶元素比当前元素小。
> 
> 尽管这个算法看起来有两个循环，看起来应该是 O(n^2) 的时间复杂度，但实际上它的时间复杂度是 O(n)。这是因为每个元素最多只进栈一次和出栈一次。也就是说，尽管内部有一个 while 循环，但该循环的总迭代次数在整个程序运行过程中最多为 n（temperatures 数组的长度）。因此，总的时间复杂度是 O(n+n) = O(2n)，我们在时间复杂度计算中通常省略常数，所以时间复杂度是 O(n)。

这是一个常见的分析时间复杂度的误区，有时候看起来有两个循环，但实际上并不意味着时间复杂度就是 O(n^2)，还需要考虑到每个元素总的处理次数。在这个问题中，每个元素的处理次数是常数，所以总的时间复杂度是线性的。这就是为什么这个解法的时间复杂度是 O(n) 而不是 O(n^2) 的原因。

```typescript
function dailyTemperatures(temperatures: number[]): number[] {
  const ans = new Array(temperatures.length).fill(0);

  const stack: number[] = [];

  for (let i = 0; i < temperatures.length; i++) {
    while (temperatures.length > 0 && temperatures[stack[stack.length - 1]] < temperatures[i]) {
      const s = stack.pop();
      ans[s] = i - s;
    }
    stack.push(i);
  }

  return ans;
};
```




