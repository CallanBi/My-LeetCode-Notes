
# 22. Generate Parentheses - 括号生成

## Tags - 题目标签

 <img src="https://img.shields.io/badge/String-字符串-blue.svg">   <img src="https://img.shields.io/badge/Dynamic Programming-动态规划-blue.svg">   <img src="https://img.shields.io/badge/Backtracking-回溯-blue.svg">  


## Description - 题目描述

### EN:
<p>Given <code>n</code> pairs of parentheses, write a function to <em>generate all combinations of well-formed parentheses</em>.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>
<pre><strong>Input:</strong> n = 3
<strong>Output:</strong> ["((()))","(()())","(())()","()(())","()()()"]
</pre><p><strong>Example 2:</strong></p>
<pre><strong>Input:</strong> n = 1
<strong>Output:</strong> ["()"]
</pre>
<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= n &lt;= 8</code></li>
</ul>


### ZH-CN:
<p>数字 <code>n</code>&nbsp;代表生成括号的对数，请你设计一个函数，用于能够生成所有可能的并且 <strong>有效的 </strong>括号组合。</p>

<p>&nbsp;</p>

<p><strong>示例 1：</strong></p>

<pre>
<strong>输入：</strong>n = 3
<strong>输出：</strong>["((()))","(()())","(())()","()(())","()()()"]
</pre>

<p><strong>示例 2：</strong></p>

<pre>
<strong>输入：</strong>n = 1
<strong>输出：</strong>["()"]
</pre>

<p>&nbsp;</p>

<p><strong>提示：</strong></p>

<ul>
	<li><code>1 &lt;= n &lt;= 8</code></li>
</ul>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/generate-parentheses/description/)  -  [LeetCode-CN](https://leetcode-cn.com/problems/generate-parentheses/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| typescript  | 60 ms | 43.8 MB | 2022/05/02 17:42 |

```typescript

function generateParenthesis(n: number): string[] {

  const res: string[] = [];

  const recur = (str: string, leftNum, rightNum) => {
    if (leftNum > n || rightNum > leftNum || rightNum > n) {
      return;
    }
    if (str.length === 2 * n) {
      res.push(str);
      return;
    }

    recur(str + '(', leftNum+1, rightNum);
    recur(str + ')', leftNum, rightNum+1);
  }

  recur('', 0, 0);

  return res;
};

```
## My Notes - 我的笔记


参考了 [这个题解](https://leetcode-cn.com/problems/generate-parentheses/solution/sui-ran-bu-shi-zui-xiu-de-dan-zhi-shao-n-0yt3/)。

思路是递归地构造出所有用 `(` 和 `)` 组成的长度为 `2n` 的字符串，在递归的过程中剪枝掉不符合要求的字符串。

有效的括号组合有个规则，是左括号数不能大于 n，且从左到右生成字符串的过程中，右括号数始终小于等于左括号数。

举个例子， 比如 `())` 这种情况，后面无论加什么括号，都绝对不是一个有效的括号组合。观察发现它的右括号数大于左括号数了。

```typescript
function generateParenthesis(n: number): string[] {

  const res: string[] = [];

  const recur = (str: string, leftNum, rightNum) => {
    if (leftNum > n || rightNum > leftNum || rightNum > n) {
      return;
    }
    if (str.length === 2 * n) {
      res.push(str);
      return;
    }

    recur(str + '(', leftNum+1, rightNum);
    recur(str + ')', leftNum, rightNum+1);
  }

  recur('', 0, 0);

  return res;
};
```


