
# 32. Longest Valid Parentheses - 最长有效括号

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Stack-栈-blue.svg">   <img src="https://img.shields.io/badge/String-字符串-blue.svg">   <img src="https://img.shields.io/badge/Dynamic Programming-动态规划-blue.svg">  


## Description - 题目描述

### EN:
<p>Given a string containing just the characters <code>&#39;(&#39;</code> and <code>&#39;)&#39;</code>, find the length of the longest valid (well-formed) parentheses substring.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>

<pre>
<strong>Input:</strong> s = &quot;(()&quot;
<strong>Output:</strong> 2
<strong>Explanation:</strong> The longest valid parentheses substring is &quot;()&quot;.
</pre>

<p><strong>Example 2:</strong></p>

<pre>
<strong>Input:</strong> s = &quot;)()())&quot;
<strong>Output:</strong> 4
<strong>Explanation:</strong> The longest valid parentheses substring is &quot;()()&quot;.
</pre>

<p><strong>Example 3:</strong></p>

<pre>
<strong>Input:</strong> s = &quot;&quot;
<strong>Output:</strong> 0
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>0 &lt;= s.length &lt;= 3 * 10<sup>4</sup></code></li>
	<li><code>s[i]</code> is <code>&#39;(&#39;</code>, or <code>&#39;)&#39;</code>.</li>
</ul>


### ZH-CN:
<p>给你一个只包含 <code>'('</code> 和 <code>')'</code> 的字符串，找出最长有效（格式正确且连续）括号子串的长度。</p>

<p> </p>

<div class="original__bRMd">
<div>
<p><strong>示例 1：</strong></p>

<pre>
<strong>输入：</strong>s = "(()"
<strong>输出：</strong>2
<strong>解释：</strong>最长有效括号子串是 "()"
</pre>

<p><strong>示例 2：</strong></p>

<pre>
<strong>输入：</strong>s = ")()())"
<strong>输出：</strong>4
<strong>解释：</strong>最长有效括号子串是 "()()"
</pre>

<p><strong>示例 3：</strong></p>

<pre>
<strong>输入：</strong>s = ""
<strong>输出：</strong>0
</pre>

<p> </p>

<p><strong>提示：</strong></p>

<ul>
	<li><code>0 <= s.length <= 3 * 10<sup>4</sup></code></li>
	<li><code>s[i]</code> 为 <code>'('</code> 或 <code>')'</code></li>
</ul>
</div>
</div>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/longest-valid-parentheses/description/)  -  [LeetCode-CN](https://leetcode.cn/problems/longest-valid-parentheses/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| typescript  | 76 ms | 44.4 MB | 2022/05/04 0:04 |

```typescript

function longestValidParentheses(s: string): number {
  const len = s.length;
  if (len === 0) {
    return 0;
  }

  const dp = new Array(len).fill(0);

  let max = 0;

  for (let i = 0; i < len; i++) {
    if (s[i] === '(') {
      continue;
    }
    if (s[i - 1] === '(') {
      dp[i] = (i >= 2 ? dp[i - 2] : 0) + 2;
    } else if (i - dp[i - 1] > 0 && s[i - dp[i - 1] - 1] === '(') {
      dp[i] = dp[i - 1] + ((i - dp[i - 1]) >= 2 ? dp[i - dp[i - 1] - 2] : 0) + 2;
    }
    max = Math.max(max, dp[i]);
  }

  return max;
};

```
## My Notes - 我的笔记


# 暴力解法（超时）

思路：对于字符串的每个子串都判断是否是有效的括号。有效的括号指每一个左括号都会有一个右括号对应，用栈来判断。

子串的长度总是偶数的。

# 动态规划

参考官方解答的视频中的讲解。

```typescript
function longestValidParentheses(s: string): number {
  const len = s.length;
  if (len === 0) {
    return 0;
  }

  const dp = new Array(len).fill(0);

  let max = 0;

  for (let i = 0; i < len; i++) {
    if (s[i] === '(') {
      continue;
    }
    if (s[i - 1] === '(') {
      dp[i] = (i >= 2 ? dp[i - 2] : 0) + 2;
    } else if (i - dp[i - 1] > 0 && s[i - dp[i - 1] - 1] === '(') {
      dp[i] = dp[i - 1] + ((i - dp[i - 1]) >= 2 ? dp[i - dp[i - 1] - 2] : 0) + 2;
    }
    max = Math.max(max, dp[i]);
  }

  return max;
};
```


