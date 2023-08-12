
# 647. Palindromic Substrings - 回文子串

## Tags - 题目标签

 <img src="https://img.shields.io/badge/String-字符串-blue.svg">   <img src="https://img.shields.io/badge/Dynamic Programming-动态规划-blue.svg">  


## Description - 题目描述

### EN:
<p>Given a string <code>s</code>, return <em>the number of <strong>palindromic substrings</strong> in it</em>.</p>

<p>A string is a <strong>palindrome</strong> when it reads the same backward as forward.</p>

<p>A <strong>substring</strong> is a contiguous sequence of characters within the string.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input:</strong> s = &quot;abc&quot;
<strong>Output:</strong> 3
<strong>Explanation:</strong> Three palindromic strings: &quot;a&quot;, &quot;b&quot;, &quot;c&quot;.
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre>
<strong>Input:</strong> s = &quot;aaa&quot;
<strong>Output:</strong> 6
<strong>Explanation:</strong> Six palindromic strings: &quot;a&quot;, &quot;a&quot;, &quot;a&quot;, &quot;aa&quot;, &quot;aa&quot;, &quot;aaa&quot;.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= s.length &lt;= 1000</code></li>
	<li><code>s</code> consists of lowercase English letters.</li>
</ul>


### ZH-CN:
<p>给你一个字符串 <code>s</code> ，请你统计并返回这个字符串中 <strong>回文子串</strong> 的数目。</p>

<p><strong>回文字符串</strong> 是正着读和倒过来读一样的字符串。</p>

<p><strong>子字符串</strong> 是字符串中的由连续字符组成的一个序列。</p>

<p>具有不同开始位置或结束位置的子串，即使是由相同的字符组成，也会被视作不同的子串。</p>

<p>&nbsp;</p>

<p><strong>示例 1：</strong></p>

<pre>
<strong>输入：</strong>s = "abc"
<strong>输出：</strong>3
<strong>解释：</strong>三个回文子串: "a", "b", "c"
</pre>

<p><strong>示例 2：</strong></p>

<pre>
<strong>输入：</strong>s = "aaa"
<strong>输出：</strong>6
<strong>解释：</strong>6个回文子串: "a", "a", "a", "aa", "aa", "aaa"</pre>

<p>&nbsp;</p>

<p><strong>提示：</strong></p>

<ul>
	<li><code>1 &lt;= s.length &lt;= 1000</code></li>
	<li><code>s</code> 由小写英文字母组成</li>
</ul>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/palindromic-substrings/description/)  -  [LeetCode-CN](https://leetcode.cn/problems/palindromic-substrings/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| typescript  | 64 ms | 42.9 MB | 2023/08/12 22:43 |

```typescript

function countSubstrings(s: string): number {
  if (s.length === 1) {
    return 1;
  }

  let count = 0;

  for (let i = 0; i < s.length; i++) {
    // 长度为奇数情况
    for (let j = 0; i + j <= s.length && i - j >= 0; j++) {
      if (s[i - j] === s[i + j]) {
        count += 1;
      } else {
        break;
      }
    }

    // 长度为偶数情况
    for (let j = 0; i + j <= s.length && i - j >= 0; j++) {
      if (s[i - j] === s[i + j + 1]) {
        count += 1;
      } else {
        break;
      }
    }
  }

  return count;
};

```
## My Notes - 我的笔记


# 中心展开法
回文串，沿着中心展开，分奇偶讨论。

```typescript
function countSubstrings(s: string): number {
  if (s.length === 1) {
    return 1;
  }

  let count = 0;

  for (let i = 0; i < s.length; i++) {
    // 长度为奇数情况
    for (let j = 0; i + j <= s.length && i - j >= 0; j++) {
      if (s[i - j] === s[i + j]) {
        count += 1;
      } else {
        break;
      }
    }

    // 长度为偶数情况
    for (let j = 0; i + j <= s.length && i - j >= 0; j++) {
      if (s[i - j] === s[i + j + 1]) {
        count += 1;
      } else {
        break;
      }
    }
  }

  return count;
};
```

