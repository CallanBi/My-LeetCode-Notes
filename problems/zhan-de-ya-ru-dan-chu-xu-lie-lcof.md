
# 剑指 Offer 31. 栈的压入、弹出序列 LCOF - 栈的压入、弹出序列

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Stack-栈-blue.svg">   <img src="https://img.shields.io/badge/Array-数组-blue.svg">   <img src="https://img.shields.io/badge/Simulation-模拟-blue.svg">  


## Description - 题目描述

### EN:
English description is not available for the problem. Please switch to Chinese.

### ZH-CN:
<p>输入两个整数序列，第一个序列表示栈的压入顺序，请判断第二个序列是否为该栈的弹出顺序。假设压入栈的所有数字均不相等。例如，序列 {1,2,3,4,5} 是某栈的压栈序列，序列 {4,5,3,2,1} 是该压栈序列对应的一个弹出序列，但 {4,3,5,1,2} 就不可能是该压栈序列的弹出序列。</p>

<p>&nbsp;</p>

<p><strong>示例 1：</strong></p>

<pre><strong>输入：</strong>pushed = [1,2,3,4,5], popped = [4,5,3,2,1]
<strong>输出：</strong>true
<strong>解释：</strong>我们可以按以下顺序执行：
push(1), push(2), push(3), push(4), pop() -&gt; 4,
push(5), pop() -&gt; 5, pop() -&gt; 3, pop() -&gt; 2, pop() -&gt; 1
</pre>

<p><strong>示例 2：</strong></p>

<pre><strong>输入：</strong>pushed = [1,2,3,4,5], popped = [4,3,5,1,2]
<strong>输出：</strong>false
<strong>解释：</strong>1 不能在 2 之前弹出。
</pre>

<p>&nbsp;</p>

<p><strong>提示：</strong></p>

<ol>
	<li><code>0 &lt;= pushed.length == popped.length &lt;= 1000</code></li>
	<li><code>0 &lt;= pushed[i], popped[i] &lt; 1000</code></li>
	<li><code>pushed</code>&nbsp;是&nbsp;<code>popped</code>&nbsp;的排列。</li>
</ol>

<p>注意：本题与主站 946 题相同：<a href="https://leetcode-cn.com/problems/validate-stack-sequences/">https://leetcode-cn.com/problems/validate-stack-sequences/</a></p>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/zhan-de-ya-ru-dan-chu-xu-lie-lcof/description/)  -  [LeetCode-CN](https://leetcode.cn/problems/zhan-de-ya-ru-dan-chu-xu-lie-lcof/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| typescript  | 76 ms | 40.5 MB | 2021/11/07 20:18 |

```typescript

function validateStackSequences(pushed: number[], popped: number[]): boolean {
  const pushedLen = pushed.length, poppedLen = popped.length;
  let i = 0, j = 0;
  const assitantStack = [];
  while (i < pushedLen) {
    while (pushed[i] !== popped[j] && i < pushedLen) {
      assitantStack.push(pushed[i]);
      i++;
    }

    if (i === pushedLen) {
      return false;
    }

    if (pushed[i] === popped[j]) {
      assitantStack.push(pushed[i]);
      i++;
    }

    if (i >= pushedLen) {
      break;
    }

    while(assitantStack[assitantStack.length-1] === popped[j] && assitantStack.length > 0) {
      assitantStack.pop();
      j++;
    }
  }

  while(assitantStack[assitantStack.length-1] === popped[j] && assitantStack.length > 0) {
    assitantStack.pop();
    j++;
  }

  if (assitantStack.length === 0 || j >= poppedLen) {
    return true;
  }
  
  return false;
};

```
## My Notes - 我的笔记


剑指 offer 的思路
```typescript
function validateStackSequences(pushed: number[], popped: number[]): boolean {
  const pushedLen = pushed.length, poppedLen = popped.length;
  let i = 0, j = 0;
  const assitantStack = [];
  while (i < pushedLen) {
    while (pushed[i] !== popped[j] && i < pushedLen) {
      assitantStack.push(pushed[i]);
      i++;
    }

    if (i === pushedLen) {
      return false;
    }

    if (pushed[i] === popped[j]) {
      assitantStack.push(pushed[i]);
      i++;
    }

    if (i >= pushedLen) {
      break;
    }

    while(assitantStack[assitantStack.length-1] === popped[j] && assitantStack.length > 0) {
      assitantStack.pop();
      j++;
    }
  }

  while(assitantStack[assitantStack.length-1] === popped[j] && assitantStack.length > 0) {
    assitantStack.pop();
    j++;
  }

  if (assitantStack.length === 0 || j >= poppedLen) {
    return true;
  }
  
  return false;
};
```
1.` pop()` + while 循环的时候要注意循环条件有 `stack.length > 0`，否则就陷入死循环中
2. 注意 `push(e)` 中分清 e 为下标还是元素，不要 `push` 了下标进去 

