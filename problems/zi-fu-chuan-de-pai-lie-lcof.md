
# 剑指 Offer 38. 字符串的排列  LCOF - 字符串的排列

## Tags - 题目标签

 <img src="https://img.shields.io/badge/String-字符串-blue.svg">   <img src="https://img.shields.io/badge/Backtracking-回溯-blue.svg">  


## Description - 题目描述

### EN:
English description is not available for the problem. Please switch to Chinese.

### ZH-CN:
<p>输入一个字符串，打印出该字符串中字符的所有排列。</p>

<p>&nbsp;</p>

<p>你可以以任意顺序返回这个字符串数组，但里面不能有重复元素。</p>

<p>&nbsp;</p>

<p><strong>示例:</strong></p>

<pre><strong>输入：</strong>s = &quot;abc&quot;
<strong>输出：[</strong>&quot;abc&quot;,&quot;acb&quot;,&quot;bac&quot;,&quot;bca&quot;,&quot;cab&quot;,&quot;cba&quot;<strong>]</strong>
</pre>

<p>&nbsp;</p>

<p><strong>限制：</strong></p>

<p><code>1 &lt;= s 的长度 &lt;= 8</code></p>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/zi-fu-chuan-de-pai-lie-lcof/description/)  -  [LeetCode-CN](https://leetcode.cn/problems/zi-fu-chuan-de-pai-lie-lcof/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| typescript  | 1440 ms | 64.3 MB | 2021/11/30 12:17 |

```typescript

function permutation(s: string): string[] {
  if (s.length === 0) {
    return [];
  }
  const allCharacter = s.split('');
  const resWithoutDedup = allCharacter.reduce((acc: string[], cur: string) => {
    if (acc.length === 0) {
      return [cur[0]];
    } else {
      return acc.reduce((innerAcc: string[], innerCur: string) => {
        const innerRes = [];
        for (let insertIdx = 0; insertIdx <= innerCur.length; insertIdx++) {
          const innerCurArr = innerCur.split('');
          innerCurArr.splice(insertIdx, 0, cur);
          const newWord = innerCurArr.join('');
          innerRes.push(newWord);
        }
        return [...innerAcc, ...innerRes];
      }, [])
    }
  }, []);
  return [...new Set(resWithoutDedup)];
};

```
## My Notes - 我的笔记


1. 最快能写出来的方法：
直接三循环暴力解，去重丢给 set 去处理
```typescript
function permutation(s: string): string[] {
  if (s.length === 0) {
    return [];
  }
  const allCharacter = s.split('');
  const resWithoutDedup = allCharacter.reduce((acc: string[], cur: string) => {
    if (acc.length === 0) {
      return [cur[0]];
    } else {
      return acc.reduce((innerAcc: string[], innerCur: string) => {
        const innerRes = [];
        for (let insertIdx = 0; insertIdx <= innerCur.length; insertIdx++) {
          const innerCurArr = innerCur.split('');
          innerCurArr.splice(insertIdx, 0, cur);
          const newWord = innerCurArr.join('');
          innerRes.push(newWord);
        }
        return [...innerAcc, ...innerRes];
      }, [])
    }
  }, [])
  return Array.from(new Set(resWithoutDedup));
};
```

2. 递归写法


