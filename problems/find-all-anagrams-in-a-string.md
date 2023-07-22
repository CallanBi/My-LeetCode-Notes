
# 438. Find All Anagrams in a String - 找到字符串中所有字母异位词

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Hash Table-哈希表-blue.svg">   <img src="https://img.shields.io/badge/String-字符串-blue.svg">   <img src="https://img.shields.io/badge/Sliding Window-滑动窗口-blue.svg">  


## Description - 题目描述

### EN:
<p>Given two strings <code>s</code> and <code>p</code>, return <em>an array of all the start indices of </em><code>p</code><em>&#39;s anagrams in </em><code>s</code>. You may return the answer in <strong>any order</strong>.</p>

<p>An <strong>Anagram</strong> is a word or phrase formed by rearranging the letters of a different word or phrase, typically using all the original letters exactly once.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input:</strong> s = &quot;cbaebabacd&quot;, p = &quot;abc&quot;
<strong>Output:</strong> [0,6]
<strong>Explanation:</strong>
The substring with start index = 0 is &quot;cba&quot;, which is an anagram of &quot;abc&quot;.
The substring with start index = 6 is &quot;bac&quot;, which is an anagram of &quot;abc&quot;.
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre>
<strong>Input:</strong> s = &quot;abab&quot;, p = &quot;ab&quot;
<strong>Output:</strong> [0,1,2]
<strong>Explanation:</strong>
The substring with start index = 0 is &quot;ab&quot;, which is an anagram of &quot;ab&quot;.
The substring with start index = 1 is &quot;ba&quot;, which is an anagram of &quot;ab&quot;.
The substring with start index = 2 is &quot;ab&quot;, which is an anagram of &quot;ab&quot;.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= s.length, p.length &lt;= 3 * 10<sup>4</sup></code></li>
	<li><code>s</code> and <code>p</code> consist of lowercase English letters.</li>
</ul>


### ZH-CN:
<p>给定两个字符串&nbsp;<code>s</code>&nbsp;和 <code>p</code>，找到&nbsp;<code>s</code><strong>&nbsp;</strong>中所有&nbsp;<code>p</code><strong>&nbsp;</strong>的&nbsp;<strong>异位词&nbsp;</strong>的子串，返回这些子串的起始索引。不考虑答案输出的顺序。</p>

<p><strong>异位词 </strong>指由相同字母重排列形成的字符串（包括相同的字符串）。</p>

<p>&nbsp;</p>

<p><strong>示例&nbsp;1:</strong></p>

<pre>
<strong>输入: </strong>s = "cbaebabacd", p = "abc"
<strong>输出: </strong>[0,6]
<strong>解释:</strong>
起始索引等于 0 的子串是 "cba", 它是 "abc" 的异位词。
起始索引等于 6 的子串是 "bac", 它是 "abc" 的异位词。
</pre>

<p><strong>&nbsp;示例 2:</strong></p>

<pre>
<strong>输入: </strong>s = "abab", p = "ab"
<strong>输出: </strong>[0,1,2]
<strong>解释:</strong>
起始索引等于 0 的子串是 "ab", 它是 "ab" 的异位词。
起始索引等于 1 的子串是 "ba", 它是 "ab" 的异位词。
起始索引等于 2 的子串是 "ab", 它是 "ab" 的异位词。
</pre>

<p>&nbsp;</p>

<p><strong>提示:</strong></p>

<ul>
	<li><code>1 &lt;= s.length, p.length &lt;= 3 * 10<sup>4</sup></code></li>
	<li><code>s</code>&nbsp;和&nbsp;<code>p</code>&nbsp;仅包含小写字母</li>
</ul>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/find-all-anagrams-in-a-string/description/)  -  [LeetCode-CN](https://leetcode.cn/problems/find-all-anagrams-in-a-string/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| typescript  | 128 ms | 47.7 MB | 2023/07/20 21:35 |

```typescript

function findAnagrams(s: string, p: string): number[] {
  let start = 0, end = 0;

  const res = [];

  let hash = {};

  for (let i = 0; i < p.length; i++) {
    hash[p[i]] = !hash[p[i]] ? [1, 0] : [hash[p[i]][0] + 1, 0];
  }

  while (start < s.length && end < s.length) {
    if (hash[s[end]]) {
      if (hash[s[end]][1] < hash[s[end]][0]) {
        hash[s[end]][1] += 1;

        if (hash[s[end]][1] === hash[s[end]][0]) {
          if (end - start + 1 === p.length) {

            res.push(start);

            hash[s[start]][1] -= 1;

            start += 1;

            end += 1;

            continue;
          }
        }
        end++;
      } else {
        let dupIdx = start;

        while (dupIdx < end) {
          if (s[dupIdx] === s[end]) {
            break;
          }
          hash[s[dupIdx]][1] -= 1;
          dupIdx++;
        }

        start = dupIdx + 1;
        end = end + 1;
      }
    } else {
      for (let i = 0; i < p.length; i++) {
        hash[p[i]][1] = 0;
      }
      start = end + 1;
      end = start;
    }
  }

  return res;
}; 

```
## My Notes - 我的笔记


思路：滑动窗口。

```typescript
function findAnagrams(s: string, p: string): number[] {
  let start = 0, end = 0;

  const res = [];

  let hash = {};

  for (let i = 0; i < p.length; i++) {
    hash[p[i]] = !hash[p[i]] ? [1, 0] : [hash[p[i]][0] + 1, 0];
  }

  while (start < s.length && end < s.length) {
    if (hash[s[end]]) {
      if (hash[s[end]][1] < hash[s[end]][0]) {
        hash[s[end]][1] += 1;

        if (hash[s[end]][1] === hash[s[end]][0]) {
          if (end - start + 1 === p.length) {

            res.push(start);
            
            hash[s[start]][1] -= 1;

            start += 1;

            end += 1;

            continue;
          }
        }
        end++;
      } else {
        // 说明 s[end] 与之前窗口的字符重复。重复字符之前的字符都不能用了，从非重复的开始寻找。
        let dupIdx = start;

        while (dupIdx < end) {
          if (s[dupIdx] === s[end]) {
            break;
          }
          hash[s[dupIdx]][1] -= 1;
          dupIdx++;
        }

        start = dupIdx + 1;
        end = end + 1;
      }
    } else {
      // clear hash
      for (let i = 0; i < p.length; i++) {
        hash[p[i]][1] = 0;
      }
      start = end + 1;
      end = start;
    }
  }

  return res;
}; 
```

