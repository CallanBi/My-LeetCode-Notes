
# 3. Longest Substring Without Repeating Characters - 无重复字符的最长子串

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Hash Table-哈希表-blue.svg">   <img src="https://img.shields.io/badge/String-字符串-blue.svg">   <img src="https://img.shields.io/badge/Sliding Window-滑动窗口-blue.svg">  


## Description - 题目描述

### EN:
<p>Given a string <code>s</code>, find the length of the <strong>longest substring</strong> without repeating characters.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>

<pre>
<strong>Input:</strong> s = &quot;abcabcbb&quot;
<strong>Output:</strong> 3
<strong>Explanation:</strong> The answer is &quot;abc&quot;, with the length of 3.
</pre>

<p><strong>Example 2:</strong></p>

<pre>
<strong>Input:</strong> s = &quot;bbbbb&quot;
<strong>Output:</strong> 1
<strong>Explanation:</strong> The answer is &quot;b&quot;, with the length of 1.
</pre>

<p><strong>Example 3:</strong></p>

<pre>
<strong>Input:</strong> s = &quot;pwwkew&quot;
<strong>Output:</strong> 3
<strong>Explanation:</strong> The answer is &quot;wke&quot;, with the length of 3.
Notice that the answer must be a substring, &quot;pwke&quot; is a subsequence and not a substring.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>0 &lt;= s.length &lt;= 5 * 10<sup>4</sup></code></li>
	<li><code>s</code> consists of English letters, digits, symbols and spaces.</li>
</ul>


### ZH-CN:
<p>给定一个字符串 <code>s</code> ，请你找出其中不含有重复字符的&nbsp;<strong>最长子串&nbsp;</strong>的长度。</p>

<p>&nbsp;</p>

<p><strong>示例&nbsp;1:</strong></p>

<pre>
<strong>输入: </strong>s = "abcabcbb"
<strong>输出: </strong>3 
<strong>解释:</strong> 因为无重复字符的最长子串是 <code>"abc"，所以其</code>长度为 3。
</pre>

<p><strong>示例 2:</strong></p>

<pre>
<strong>输入: </strong>s = "bbbbb"
<strong>输出: </strong>1
<strong>解释: </strong>因为无重复字符的最长子串是 <code>"b"</code>，所以其长度为 1。
</pre>

<p><strong>示例 3:</strong></p>

<pre>
<strong>输入: </strong>s = "pwwkew"
<strong>输出: </strong>3
<strong>解释: </strong>因为无重复字符的最长子串是&nbsp;<code>"wke"</code>，所以其长度为 3。
&nbsp;    请注意，你的答案必须是 <strong>子串 </strong>的长度，<code>"pwke"</code>&nbsp;是一个<em>子序列，</em>不是子串。
</pre>

<p>&nbsp;</p>

<p><strong>提示：</strong></p>

<ul>
	<li><code>0 &lt;= s.length &lt;= 5 * 10<sup>4</sup></code></li>
	<li><code>s</code>&nbsp;由英文字母、数字、符号和空格组成</li>
</ul>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/longest-substring-without-repeating-characters/description/)  -  [LeetCode-CN](https://leetcode-cn.com/problems/longest-substring-without-repeating-characters/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| typescript  | 88 ms | 48.6 MB | 2022/03/31 19:30 |

```typescript

function lengthOfLongestSubstring(s: string): number {
  let window = '';
  let max = 0;
  for (let e of s.split('')) {
    const idx = window.indexOf(e);
    if (idx === -1) {
      window = window + e;
    } else {
      max = max > window.length ? max : window.length;
      window = window.slice(idx + 1) + e;
    }
  }
  max = Math.max(window.length, max);

  return max;
};

```
## My Notes - 我的笔记


# 滑动窗口

令 window 为一个滑动窗口，window 用字符串来表达。最初为`''`。

感觉字符串问题的滑动窗口都可以用字符串来表达。就可以省去很多用指针 `i`，`j` 去截取滑动窗口的烦恼。

接着对输入的 s 进行遍历。（技巧：将字符串 `split()` 后进行遍历）。

对于每个元素 e：

如果不存在 e，滑动窗口就加上 e；

如果存在e：

将滑动窗口长度与当前记录的最大值比较，取最大的。

然后滑动窗口开始变化，这个是关键。

只需要找到滑动窗口中 e 的位置，然后滑动窗口变为`${window.slice(idx + 1)}${e}`即可。

当前滑动窗口中与 s 的重复元素的后一个位置到当前滑动窗口末尾元素和当前元素的拼接，作为新的滑动窗口。

以 `abcbdfg` 为例，当遍历到 `s[3]` 时，新的滑动窗口变为`cb`。也就是`abc.slice(2) + 'b'`，2 就是 `b 在滑动窗口的位置 + 1`。

`slice()`可以不用考虑越界问题。以`abccdef` 为例，`abc.slice(2 + 1)` 为空字符串，再接上 c 的话，滑动窗口为`c`，符合预期。

```typescript
function lengthOfLongestSubstring(s: string): number {
  let window = '';
  let max = 0;
  for (let e of s.split('')) {
    const idx = window.indexOf(e);
    if (idx === -1) {
      window = window + e;
    } else {
      max = max > window.length ? max : window.length;
      window = window.slice(idx + 1) + e;
    }
  }
  max = Math.max(window.length, max);

  return max;
};
```



和剑指 offer 中的某道题一样，也可以用**动态规划+哈希表**做：

```typescript
function lengthOfLongestSubstring(s: string): number {
  const len = s.length;
  if (len <= 2) {
    if (len === 2 && s[0] === s[1]) {
      return 1;
    } else {
      return len;
    }
  }
  const dp = new Array(len).fill(0);
  dp[0] = 1, dp[1] = s[0] === s[1] ? 1 : 2;
  const nearestHash = new Map<string, number>();
  nearestHash.set(s[0], 0);
  nearestHash.set(s[1], 1);
  for (let i = 2; i < len; i++) {
    const nearestSameLetterPos = nearestHash.get(s[i]) ?? -1;
    if (nearestSameLetterPos !== -1) {
      if (i - nearestSameLetterPos > dp[i-1]) {
        dp[i] = dp[i-1] + 1;
      } else {
        dp[i] = i - nearestSameLetterPos;
      }
    } else {
      dp[i] = dp[i-1] + 1;
    }
    nearestHash.set(s[i], i);
  }
  return Math.max(...dp);
};
```


