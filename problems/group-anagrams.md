
# 49. Group Anagrams - 字母异位词分组

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Hash Table-哈希表-blue.svg">   <img src="https://img.shields.io/badge/String-字符串-blue.svg">   <img src="https://img.shields.io/badge/Sorting-排序-blue.svg">  


## Description - 题目描述

### EN:
<p>Given an array of strings <code>strs</code>, group <strong>the anagrams</strong> together. You can return the answer in <strong>any order</strong>.</p>

<p>An <strong>Anagram</strong> is a word or phrase formed by rearranging the letters of a different word or phrase, typically using all the original letters exactly once.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>
<pre><strong>Input:</strong> strs = ["eat","tea","tan","ate","nat","bat"]
<strong>Output:</strong> [["bat"],["nat","tan"],["ate","eat","tea"]]
</pre><p><strong>Example 2:</strong></p>
<pre><strong>Input:</strong> strs = [""]
<strong>Output:</strong> [[""]]
</pre><p><strong>Example 3:</strong></p>
<pre><strong>Input:</strong> strs = ["a"]
<strong>Output:</strong> [["a"]]
</pre>
<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= strs.length &lt;= 10<sup>4</sup></code></li>
	<li><code>0 &lt;= strs[i].length &lt;= 100</code></li>
	<li><code>strs[i]</code> consists of lowercase English letters.</li>
</ul>


### ZH-CN:
<p>给你一个字符串数组，请你将 <strong>字母异位词</strong> 组合在一起。可以按任意顺序返回结果列表。</p>

<p><strong>字母异位词</strong> 是由重新排列源单词的字母得到的一个新单词，所有源单词中的字母通常恰好只用一次。</p>

<p>&nbsp;</p>

<p><strong>示例 1:</strong></p>

<pre>
<strong>输入:</strong> strs = <code>["eat", "tea", "tan", "ate", "nat", "bat"]</code>
<strong>输出: </strong>[["bat"],["nat","tan"],["ate","eat","tea"]]</pre>

<p><strong>示例 2:</strong></p>

<pre>
<strong>输入:</strong> strs = <code>[""]</code>
<strong>输出: </strong>[[""]]
</pre>

<p><strong>示例 3:</strong></p>

<pre>
<strong>输入:</strong> strs = <code>["a"]</code>
<strong>输出: </strong>[["a"]]</pre>

<p>&nbsp;</p>

<p><strong>提示：</strong></p>

<ul>
	<li><code>1 &lt;= strs.length &lt;= 10<sup>4</sup></code></li>
	<li><code>0 &lt;= strs[i].length &lt;= 100</code></li>
	<li><code>strs[i]</code>&nbsp;仅包含小写字母</li>
</ul>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/group-anagrams/description/)  -  [LeetCode-CN](https://leetcode.cn/problems/group-anagrams/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| typescript  | 112 ms | 53 MB | 2022/05/11 19:25 |

```typescript

function groupAnagrams(strs: string[]): string[][] {
  const map: Record<string, string[]> = {};

  strs.forEach(e => {
    const hash: number[] = new Array(26).fill(0);
    for(let i = 0; i < e.length; i++) {
      hash[e[i].charCodeAt(0) - 'a'.charCodeAt(0)]++;
    }
    const key = hash.toString();
    if (map[key]) {
      map[key].push(e);
    } else {
      map[key] = [e];
    }
  })

  return Object.values(map);
};

```
## My Notes - 我的笔记


参考官方题解的思路。

# 解法1：对字符串进行排序，相等的放到一组
```typescript
function groupAnagrams(strs: string[]): string[][] {
  const len = strs.length, ans = new Map()
  for (let i = 0; i < len; i++) {
    let asc = strs[i].split('').map(c => c.charCodeAt(0)).sort().join()
    if (ans.has(asc)) {
      ans.get(asc).push(strs[i])
    } else {
      ans.set(asc, [strs[i]])
    }
  }
  return Array.from(ans.values())
};

```

# 解法2：以所有单词单词出现的次数作为哈希，相同的放到一组
技巧：JS 中可以给 `Object` 属性设置为一个数组，这个数组会调用这个数组实例的 `toString()` 方法。(在 ts 中要显式调用 `toString()`)。

```typescript
function groupAnagrams(strs: string[]): string[][] {
  const map: Record<string, string[]> = {};

  strs.forEach(e => {
    const hash: number[] = new Array(26).fill(0);
    for(let i = 0; i < e.length; i++) {
      hash[e[i].charCodeAt(0) - 'a'.charCodeAt(0)]++;
    }
    const key = hash.toString();
    if (map[key]) {
      map[key].push(e);
    } else {
      map[key] = [e];
    }
  })

  return Object.values(map);
};
```



