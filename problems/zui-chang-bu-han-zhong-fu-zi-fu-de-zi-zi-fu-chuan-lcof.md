
# 剑指 Offer 48. 最长不含重复字符的子字符串 LCOF - 最长不含重复字符的子字符串

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Hash Table-哈希表-blue.svg">   <img src="https://img.shields.io/badge/String-字符串-blue.svg">   <img src="https://img.shields.io/badge/Sliding Window-滑动窗口-blue.svg">  


## Description - 题目描述

### EN:
English description is not available for the problem. Please switch to Chinese.

### ZH-CN:
<p>请从字符串中找出一个最长的不包含重复字符的子字符串，计算该最长子字符串的长度。</p>

<p>&nbsp;</p>

<p><strong>示例&nbsp;1:</strong></p>

<pre><strong>输入: </strong>&quot;abcabcbb&quot;
<strong>输出: </strong>3 
<strong>解释:</strong> 因为无重复字符的最长子串是 <code>&quot;abc&quot;，所以其</code>长度为 3。
</pre>

<p><strong>示例 2:</strong></p>

<pre><strong>输入: </strong>&quot;bbbbb&quot;
<strong>输出: </strong>1
<strong>解释: </strong>因为无重复字符的最长子串是 <code>&quot;b&quot;</code>，所以其长度为 1。
</pre>

<p><strong>示例 3:</strong></p>

<pre><strong>输入: </strong>&quot;pwwkew&quot;
<strong>输出: </strong>3
<strong>解释: </strong>因为无重复字符的最长子串是&nbsp;<code>&quot;wke&quot;</code>，所以其长度为 3。
&nbsp;    请注意，你的答案必须是 <strong>子串 </strong>的长度，<code>&quot;pwke&quot;</code>&nbsp;是一个<em>子序列，</em>不是子串。
</pre>

<p>&nbsp;</p>

<p>提示：</p>

<ul>
	<li><code>s.length &lt;= 40000</code></li>
</ul>

<p>注意：本题与主站 3 题相同：<a href="https://leetcode-cn.com/problems/longest-substring-without-repeating-characters/">https://leetcode-cn.com/problems/longest-substring-without-repeating-characters/</a></p>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/zui-chang-bu-han-zhong-fu-zi-fu-de-zi-zi-fu-chuan-lcof/description/)  -  [LeetCode-CN](https://leetcode.cn/problems/zui-chang-bu-han-zhong-fu-zi-fu-de-zi-zi-fu-chuan-lcof/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| typescript  | 100 ms | 42.7 MB | 2021/12/19 15:22 |

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
## My Notes - 我的笔记


# 动态规划+哈希表


