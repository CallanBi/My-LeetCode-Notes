
# 剑指 Offer 58 - II. 左旋转字符串 LCOF - 左旋转字符串

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Math-数学-blue.svg">   <img src="https://img.shields.io/badge/Two Pointers-双指针-blue.svg">   <img src="https://img.shields.io/badge/String-字符串-blue.svg">  


## Description - 题目描述

### EN:
<p>English description is not available for the problem. Please switch to Chinese.</p>


### ZH-CN:
<p>字符串的左旋转操作是把字符串前面的若干个字符转移到字符串的尾部。请定义一个函数实现字符串左旋转操作的功能。比如，输入字符串&quot;abcdefg&quot;和数字2，该函数将返回左旋转两位得到的结果&quot;cdefgab&quot;。</p>

<p>&nbsp;</p>

<p><strong>示例 1：</strong></p>

<pre><strong>输入:</strong> s = &quot;abcdefg&quot;, k = 2
<strong>输出:&nbsp;</strong>&quot;cdefgab&quot;
</pre>

<p><strong>示例 2：</strong></p>

<pre><strong>输入:</strong> s = &quot;lrloseumgh&quot;, k = 6
<strong>输出:&nbsp;</strong>&quot;umghlrlose&quot;
</pre>

<p>&nbsp;</p>

<p><strong>限制：</strong></p>

<ul>
	<li><code>1 &lt;= k &lt; s.length &lt;= 10000</code></li>
</ul>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/zuo-xuan-zhuan-zi-fu-chuan-lcof/description/)  -  [LeetCode-CN](https://leetcode-cn.com/problems/zuo-xuan-zhuan-zi-fu-chuan-lcof/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| typescript  | 64 ms | 46.1 MB | 2022/04/23 16:50 |

```typescript

function reverseLeftWords(s: string, n: number): string {
  let sArr = s.split('');
  const sliced = sArr.slice(0, n);
  sArr.splice(0, n);

  sArr = [...sArr, ...sliced];

  return sArr.join('');

};

```
## My Notes - 我的笔记


还是用内置函数即可。

