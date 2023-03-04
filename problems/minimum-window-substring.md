
# 76. Minimum Window Substring - 最小覆盖子串

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Hash Table-哈希表-blue.svg">   <img src="https://img.shields.io/badge/String-字符串-blue.svg">   <img src="https://img.shields.io/badge/Sliding Window-滑动窗口-blue.svg">  


## Description - 题目描述

### EN:
<p>Given two strings <code>s</code> and <code>t</code> of lengths <code>m</code> and <code>n</code> respectively, return <em>the <strong>minimum window</strong></em> <span data-keyword="substring-nonempty"><strong><em>substring</em></strong></span><em> of </em><code>s</code><em> such that every character in </em><code>t</code><em> (<strong>including duplicates</strong>) is included in the window</em>. If there is no such substring, return <em>the empty string </em><code>&quot;&quot;</code>.</p>

<p>The testcases will be generated such that the answer is <strong>unique</strong>.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input:</strong> s = &quot;ADOBECODEBANC&quot;, t = &quot;ABC&quot;
<strong>Output:</strong> &quot;BANC&quot;
<strong>Explanation:</strong> The minimum window substring &quot;BANC&quot; includes &#39;A&#39;, &#39;B&#39;, and &#39;C&#39; from string t.
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre>
<strong>Input:</strong> s = &quot;a&quot;, t = &quot;a&quot;
<strong>Output:</strong> &quot;a&quot;
<strong>Explanation:</strong> The entire string s is the minimum window.
</pre>

<p><strong class="example">Example 3:</strong></p>

<pre>
<strong>Input:</strong> s = &quot;a&quot;, t = &quot;aa&quot;
<strong>Output:</strong> &quot;&quot;
<strong>Explanation:</strong> Both &#39;a&#39;s from t must be included in the window.
Since the largest window of s only has one &#39;a&#39;, return empty string.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>m == s.length</code></li>
	<li><code>n == t.length</code></li>
	<li><code>1 &lt;= m, n &lt;= 10<sup>5</sup></code></li>
	<li><code>s</code> and <code>t</code> consist of uppercase and lowercase English letters.</li>
</ul>

<p>&nbsp;</p>
<p><strong>Follow up:</strong> Could you find an algorithm that runs in <code>O(m + n)</code> time?</p>


### ZH-CN:
<p>给你一个字符串 <code>s</code> 、一个字符串 <code>t</code> 。返回 <code>s</code> 中涵盖 <code>t</code> 所有字符的最小子串。如果 <code>s</code> 中不存在涵盖 <code>t</code> 所有字符的子串，则返回空字符串 <code>""</code> 。</p>

<p>&nbsp;</p>

<p><strong>注意：</strong></p>

<ul>
	<li>对于 <code>t</code> 中重复字符，我们寻找的子字符串中该字符数量必须不少于 <code>t</code> 中该字符数量。</li>
	<li>如果 <code>s</code> 中存在这样的子串，我们保证它是唯一的答案。</li>
</ul>

<p>&nbsp;</p>

<p><strong>示例 1：</strong></p>

<pre>
<strong>输入：</strong>s = "ADOBECODEBANC", t = "ABC"
<strong>输出：</strong>"BANC"
<strong>解释：</strong>最小覆盖子串 "BANC" 包含来自字符串 t 的 'A'、'B' 和 'C'。
</pre>

<p><strong>示例 2：</strong></p>

<pre>
<strong>输入：</strong>s = "a", t = "a"
<strong>输出：</strong>"a"
<strong>解释：</strong>整个字符串 s 是最小覆盖子串。
</pre>

<p><strong>示例 3:</strong></p>

<pre>
<strong>输入:</strong> s = "a", t = "aa"
<strong>输出:</strong> ""
<strong>解释:</strong> t 中两个字符 'a' 均应包含在 s 的子串中，
因此没有符合条件的子字符串，返回空字符串。</pre>

<p>&nbsp;</p>

<p><strong>提示：</strong></p>

<ul>
	<li><code><sup>m == s.length</sup></code></li>
	<li><code><sup>n == t.length</sup></code></li>
	<li><code>1 &lt;= m, n &lt;= 10<sup>5</sup></code></li>
	<li><code>s</code> 和 <code>t</code> 由英文字母组成</li>
</ul>

<p>&nbsp;</p>
<strong>进阶：</strong>你能设计一个在 <code>o(m+n)</code> 时间内解决此问题的算法吗？


## Link - 题目链接

[LeetCode](https://leetcode.com/problems/minimum-window-substring/description/)  -  [LeetCode-CN](https://leetcode.cn/problems/minimum-window-substring/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| typescript  | 1056 ms | 50.1 MB | 2022/05/30 17:50 |

```typescript

function minWindow(s: string, t: string): string {
  if (s.length < t.length) {
    return '';
  }

  const tMap: Record<string, number> = {};

  let min = +Infinity;

  let res = '';

  let window = '';

  const windowMap: Record<string, number> = {};

  for (let i = 0; i < t.length; i++) {
    tMap[t[i]] = tMap[t[i]] ? tMap[t[i]] + 1 : 1;
  }

  function isValid(): boolean {
    let flag = true;
    const iter = Object.entries(tMap);

    for (let i = 0; i < iter.length; i++) {
      const [k, v] = iter[i];

      if (windowMap[k] === undefined) {
        flag = false;
        break;
      }
      
      if (v > windowMap[k]) {
        flag = false;
        break;
      }
    }

    return flag;
  }

  let start = 0, end = 1;

  window = s.slice(start, end);

  windowMap[window[0]] = 1;

  while (start <= end && end <= s.length) {
    if (isValid()) {
      if (window.length < min) {
        res = window;
        min = window.length;
      }
      const cnt = windowMap[window[0]];
      windowMap[window[0]] = cnt - 1;
      start++;
      window = s.slice(start, end);
    } else {
      end++;
      window = s.slice(start, end);
      const last = window[window.length - 1];
      windowMap[last] = windowMap[last] ? windowMap[last] + 1 : 1;
    }
  }

  return res;
};

```
## My Notes - 我的笔记


参考[官方题解](https://leetcode.cn/problems/minimum-window-substring/solution/zui-xiao-fu-gai-zi-chuan-by-leetcode-solution/)的滑动窗口法写的解法：
```typescript
function minWindow(s: string, t: string): string {
  if (s.length < t.length) {
    return '';
  }

  const tMap: Record<string, number> = {};

  let min = +Infinity;

  let res = '';

  let window = '';

  const sMap: Record<string, number> = {};

  for (let i = 0; i < t.length; i++) {
    tMap[t[i]] = tMap[t[i]] ? tMap[t[i]] + 1 : 1;
  }

  function isValid(): boolean {
    let flag = true;
    const iter = Object.entries(tMap);

    for (let i = 0; i < iter.length; i++) {
      const [k, v] = iter[i];

      if (sMap[k] === undefined) {
        flag = false;
        break;
      }
      
      if (v > sMap[k]) {
        flag = false;
        break;
      }
    }

    return flag;
  }

  let start = 0, end = 1;

  window = s.slice(start, end);

  sMap[window[0]] = 1;

  while (start <= end && end <= s.length) {
    if (isValid()) {
      if (window.length < min) {
        res = window;
        min = window.length;
      }
      const cnt = sMap[window[0]];
      sMap[window[0]] = cnt - 1;
      start++;
      window = s.slice(start, end);
    } else {
      end++;
      window = s.slice(start, end);
      const last = window[window.length - 1];
      sMap[last] = sMap[last] ? sMap[last] + 1 : 1;
    }
  }

  return res;
};
```

讲道理时间复杂度是一样的，我也不知道为什么执行用时那么长...

> 时间复杂度：最坏情况下左右指针对 $s$ 的每个元素各遍历一遍，哈希表中对 $s$ 中的每个元素各插入、删除一次，对 $t$ 中的元素各插入一次。每次检查是否可行会遍历整个 $t$ 的哈希表，哈希表的大小与字符集的大小有关，设字符集大小为 $C$，则渐进时间复杂度为 $O(C⋅∣s∣+∣t∣)$。
空间复杂度：这里用了两张哈希表作为辅助空间，每张哈希表最多不会存放超过字符集大小的键值对，我们设字符集大小为 $C$ ，则渐进空间复杂度为 $O(C)$。


