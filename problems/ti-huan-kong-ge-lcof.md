
# 剑指 Offer 05. 替换空格 LCOF - 替换空格

## Tags - 题目标签

 <img src="https://img.shields.io/badge/String-字符串-blue.svg">  


## Description - 题目描述

### EN:
<p>English description is not available for the problem. Please switch to Chinese.</p>


### ZH-CN:
<p>请实现一个函数，把字符串 <code>s</code> 中的每个空格替换成&quot;%20&quot;。</p>

<p>&nbsp;</p>

<p><strong>示例 1：</strong></p>

<pre><strong>输入：</strong>s = &quot;We are happy.&quot;
<strong>输出：</strong>&quot;We%20are%20happy.&quot;</pre>

<p>&nbsp;</p>

<p><strong>限制：</strong></p>

<p><code>0 &lt;= s 的长度 &lt;= 10000</code></p>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/ti-huan-kong-ge-lcof/description/)  -  [LeetCode-CN](https://leetcode-cn.com/problems/ti-huan-kong-ge-lcof/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| typescript  | 84 ms | 39.1 MB | 2021/04/03 22:21 |

```typescript

function replaceSpace(s: string): string {
  return s.replace(/ /g, '%20')
};

```
## My Notes - 我的笔记


剑指 offer 的最优解法是从后往前移动数字。
在合并两个数组（或字符串）时，如果从前往后复制每个数字（或字符）需要重复移动数字（或字符）多次，可以考虑从后往前复制，减少移动次数

