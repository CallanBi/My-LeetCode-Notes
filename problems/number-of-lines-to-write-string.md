
# 806. Number of Lines To Write String - 写字符串需要的行数

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Array-数组-blue.svg">   <img src="https://img.shields.io/badge/String-字符串-blue.svg">  


## Description - 题目描述

### EN:
<p>You are given a string <code>s</code> of lowercase English letters and an array <code>widths</code> denoting <strong>how many pixels wide</strong> each lowercase English letter is. Specifically, <code>widths[0]</code> is the width of <code>&#39;a&#39;</code>, <code>widths[1]</code> is the width of <code>&#39;b&#39;</code>, and so on.</p>

<p>You are trying to write <code>s</code> across several lines, where <strong>each line is no longer than </strong><code>100</code><strong> pixels</strong>. Starting at the beginning of <code>s</code>, write as many letters on the first line such that the total width does not exceed <code>100</code> pixels. Then, from where you stopped in <code>s</code>, continue writing as many letters as you can on the second line. Continue this process until you have written all of <code>s</code>.</p>

<p>Return <em>an array </em><code>result</code><em> of length 2 where:</em></p>

<ul>
	<li><code>result[0]</code><em> is the total number of lines.</em></li>
	<li><code>result[1]</code><em> is the width of the last line in pixels.</em></li>
</ul>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input:</strong> widths = [10,10,10,10,10,10,10,10,10,10,10,10,10,10,10,10,10,10,10,10,10,10,10,10,10,10], s = &quot;abcdefghijklmnopqrstuvwxyz&quot;
<strong>Output:</strong> [3,60]
<strong>Explanation:</strong> You can write s as follows:
abcdefghij  // 100 pixels wide
klmnopqrst  // 100 pixels wide
uvwxyz      // 60 pixels wide
There are a total of 3 lines, and the last line is 60 pixels wide.</pre>

<p><strong class="example">Example 2:</strong></p>

<pre>
<strong>Input:</strong> widths = [4,10,10,10,10,10,10,10,10,10,10,10,10,10,10,10,10,10,10,10,10,10,10,10,10,10], s = &quot;bbbcccdddaaa&quot;
<strong>Output:</strong> [2,4]
<strong>Explanation:</strong> You can write s as follows:
bbbcccdddaa  // 98 pixels wide
a            // 4 pixels wide
There are a total of 2 lines, and the last line is 4 pixels wide.</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>widths.length == 26</code></li>
	<li><code>2 &lt;= widths[i] &lt;= 10</code></li>
	<li><code>1 &lt;= s.length &lt;= 1000</code></li>
	<li><code>s</code> contains only lowercase English letters.</li>
</ul>


### ZH-CN:
<p>我们要把给定的字符串 <code>S</code>&nbsp;从左到右写到每一行上，每一行的最大宽度为100个单位，如果我们在写某个字母的时候会使这行超过了100 个单位，那么我们应该把这个字母写到下一行。我们给定了一个数组&nbsp;<code>widths</code>&nbsp;，这个数组&nbsp;widths[0] 代表 &#39;a&#39; 需要的单位，&nbsp;widths[1] 代表 &#39;b&#39; 需要的单位，...，&nbsp;widths[25] 代表 &#39;z&#39; 需要的单位。</p>

<p>现在回答两个问题：至少多少行能放下<code>S</code>，以及最后一行使用的宽度是多少个单位？将你的答案作为长度为2的整数列表返回。</p>

<pre>
<strong>示例 1:</strong>
<strong>输入:</strong> 
widths = [10,10,10,10,10,10,10,10,10,10,10,10,10,10,10,10,10,10,10,10,10,10,10,10,10,10]
S = &quot;abcdefghijklmnopqrstuvwxyz&quot;
<strong>输出:</strong> [3, 60]
<strong>解释: 
</strong>所有的字符拥有相同的占用单位10。所以书写所有的26个字母，
我们需要2个整行和占用60个单位的一行。
</pre>

<pre>
<strong>示例 2:</strong>
<strong>输入:</strong> 
widths = [4,10,10,10,10,10,10,10,10,10,10,10,10,10,10,10,10,10,10,10,10,10,10,10,10,10]
S = &quot;bbbcccdddaaa&quot;
<strong>输出:</strong> [2, 4]
<strong>解释: 
</strong>除去字母&#39;a&#39;所有的字符都是相同的单位10，并且字符串 &quot;bbbcccdddaa&quot; 将会覆盖 9 * 10 + 2 * 4 = 98 个单位.
最后一个字母 &#39;a&#39; 将会被写到第二行，因为第一行只剩下2个单位了。
所以，这个答案是2行，第二行有4个单位宽度。
</pre>

<p>&nbsp;</p>

<p><strong>注:</strong></p>

<ul>
	<li>字符串&nbsp;<code>S</code> 的长度在&nbsp;[1, 1000] 的范围。</li>
	<li><code>S</code> 只包含小写字母。</li>
	<li><code>widths</code> 是长度为&nbsp;<code>26</code>的数组。</li>
	<li><code>widths[i]</code>&nbsp;值的范围在&nbsp;<code>[2, 10]</code>。</li>
</ul>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/number-of-lines-to-write-string/description/)  -  [LeetCode-CN](https://leetcode.cn/problems/number-of-lines-to-write-string/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| typescript  | 64 ms | 42.4 MB | 2022/04/12 11:09 |

```typescript

function numberOfLines(widths: number[], s: string): number[] {
  let rowCnt = 1, curRowWidth = 0;
  for (let i = 0; i < s.length; i++) {
    const curWidth = widths[s[i].charCodeAt(0) - 'a'.charCodeAt(0)];
    if (curRowWidth + curWidth > 100) {
      rowCnt++;
      curRowWidth = curWidth;
    } else {
      curRowWidth += curWidth;
    }
  }

  return [rowCnt, curRowWidth]
};

```
## My Notes - 我的笔记


No notes

