
# 剑指 Offer 50. 第一个只出现一次的字符  LCOF - 第一个只出现一次的字符

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Queue-队列-blue.svg">   <img src="https://img.shields.io/badge/Hash Table-哈希表-blue.svg">   <img src="https://img.shields.io/badge/String-字符串-blue.svg">   <img src="https://img.shields.io/badge/Counting-计数-blue.svg">  


## Description - 题目描述

### EN:
English description is not available for the problem. Please switch to Chinese.

### ZH-CN:
<p>在字符串 s 中找出第一个只出现一次的字符。如果没有，返回一个单空格。 s 只包含小写字母。</p>

<p><strong>示例 1:</strong></p>

<pre>
输入：s = "abaccdeff"
输出：'b'
</pre>

<p><strong>示例 2:</strong></p>

<pre>
输入：s = "" 
输出：' '
</pre>

<p>&nbsp;</p>

<p><strong>限制：</strong></p>

<p><code>0 &lt;= s 的长度 &lt;= 50000</code></p>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/di-yi-ge-zhi-chu-xian-yi-ci-de-zi-fu-lcof/description/)  -  [LeetCode-CN](https://leetcode.cn/problems/di-yi-ge-zhi-chu-xian-yi-ci-de-zi-fu-lcof/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| typescript  | 108 ms | 41 MB | 2021/12/21 12:59 |

```typescript

type IdxObj = Record<string, number>;
function firstUniqChar(s: string): string {
  const characterIdx: IdxObj = {};
  const prevCharacterGroup = new Set<string>();
  for (let i = 0; i < s.length; i++) {
    if (!prevCharacterGroup.has(s[i])) {
      characterIdx[s[i]] = i;
      prevCharacterGroup.add(s[i]);
    } else {
      delete characterIdx[s[i]];
    }
  }
  let res = ' ', smallestIdx = null;
  for (let [char, idx] of Object.entries(characterIdx)) {
    if (smallestIdx === null || idx < smallestIdx) {
      res = char;
      smallestIdx = idx;
    }
  }
  return res;
};

```
## My Notes - 我的笔记


思路：维护一个对象，遍历字符串，在对象中记录索引。对象没有字符对应索引，则记录，有的话，从对象中删除。同时维护一个集合记录已经遍历过的字符，避免重复记录到对象中。

再遍历对象属性找到索引最小的即可。

