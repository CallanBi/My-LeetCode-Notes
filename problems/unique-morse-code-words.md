
# 804. Unique Morse Code Words - 唯一摩尔斯密码词

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Array-数组-blue.svg">   <img src="https://img.shields.io/badge/Hash Table-哈希表-blue.svg">   <img src="https://img.shields.io/badge/String-字符串-blue.svg">  


## Description - 题目描述

### EN:
<p>International Morse Code defines a standard encoding where each letter is mapped to a series of dots and dashes, as follows:</p>

<ul>
	<li><code>&#39;a&#39;</code> maps to <code>&quot;.-&quot;</code>,</li>
	<li><code>&#39;b&#39;</code> maps to <code>&quot;-...&quot;</code>,</li>
	<li><code>&#39;c&#39;</code> maps to <code>&quot;-.-.&quot;</code>, and so on.</li>
</ul>

<p>For convenience, the full table for the <code>26</code> letters of the English alphabet is given below:</p>

<pre>
[&quot;.-&quot;,&quot;-...&quot;,&quot;-.-.&quot;,&quot;-..&quot;,&quot;.&quot;,&quot;..-.&quot;,&quot;--.&quot;,&quot;....&quot;,&quot;..&quot;,&quot;.---&quot;,&quot;-.-&quot;,&quot;.-..&quot;,&quot;--&quot;,&quot;-.&quot;,&quot;---&quot;,&quot;.--.&quot;,&quot;--.-&quot;,&quot;.-.&quot;,&quot;...&quot;,&quot;-&quot;,&quot;..-&quot;,&quot;...-&quot;,&quot;.--&quot;,&quot;-..-&quot;,&quot;-.--&quot;,&quot;--..&quot;]</pre>

<p>Given an array of strings <code>words</code> where each word can be written as a concatenation of the Morse code of each letter.</p>

<ul>
	<li>For example, <code>&quot;cab&quot;</code> can be written as <code>&quot;-.-..--...&quot;</code>, which is the concatenation of <code>&quot;-.-.&quot;</code>, <code>&quot;.-&quot;</code>, and <code>&quot;-...&quot;</code>. We will call such a concatenation the <strong>transformation</strong> of a word.</li>
</ul>

<p>Return <em>the number of different <strong>transformations</strong> among all words we have</em>.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input:</strong> words = [&quot;gin&quot;,&quot;zen&quot;,&quot;gig&quot;,&quot;msg&quot;]
<strong>Output:</strong> 2
<strong>Explanation:</strong> The transformation of each word is:
&quot;gin&quot; -&gt; &quot;--...-.&quot;
&quot;zen&quot; -&gt; &quot;--...-.&quot;
&quot;gig&quot; -&gt; &quot;--...--.&quot;
&quot;msg&quot; -&gt; &quot;--...--.&quot;
There are 2 different transformations: &quot;--...-.&quot; and &quot;--...--.&quot;.
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre>
<strong>Input:</strong> words = [&quot;a&quot;]
<strong>Output:</strong> 1
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= words.length &lt;= 100</code></li>
	<li><code>1 &lt;= words[i].length &lt;= 12</code></li>
	<li><code>words[i]</code> consists of lowercase English letters.</li>
</ul>


### ZH-CN:
<p>国际摩尔斯密码定义一种标准编码方式，将每个字母对应于一个由一系列点和短线组成的字符串，&nbsp;比如:</p>

<ul>
	<li><code>'a'</code> 对应 <code>".-"</code> ，</li>
	<li><code>'b'</code> 对应 <code>"-..."</code> ，</li>
	<li><code>'c'</code> 对应 <code>"-.-."</code> ，以此类推。</li>
</ul>

<p>为了方便，所有 <code>26</code> 个英文字母的摩尔斯密码表如下：</p>

<pre>
[".-","-...","-.-.","-..",".","..-.","--.","....","..",".---","-.-",".-..","--","-.","---",".--.","--.-",".-.","...","-","..-","...-",".--","-..-","-.--","--.."]</pre>

<p>给你一个字符串数组 <code>words</code> ，每个单词可以写成每个字母对应摩尔斯密码的组合。</p>

<ul>
	<li>例如，<code>"cab"</code> 可以写成 <code>"-.-..--..."</code> ，(即 <code>"-.-."</code> + <code>".-"</code> + <code>"-..."</code> 字符串的结合)。我们将这样一个连接过程称作 <strong>单词翻译</strong> 。</li>
</ul>

<p>对<strong> </strong><code>words</code> 中所有单词进行单词翻译，返回不同 <strong>单词翻译</strong> 的数量。</p>

<p>&nbsp;</p>

<p><strong>示例 1：</strong></p>

<pre>
<strong>输入:</strong> words = ["gin", "zen", "gig", "msg"]
<strong>输出:</strong> 2
<strong>解释: </strong>
各单词翻译如下:
"gin" -&gt; "--...-."
"zen" -&gt; "--...-."
"gig" -&gt; "--...--."
"msg" -&gt; "--...--."

共有 2 种不同翻译, "--...-." 和 "--...--.".
</pre>

<p><strong>示例 2：</strong></p>

<pre>
<strong>输入：</strong>words = ["a"]
<strong>输出：</strong>1
</pre>

<p>&nbsp;</p>

<p><strong>提示：</strong></p>

<ul>
	<li><code>1 &lt;= words.length &lt;= 100</code></li>
	<li><code>1 &lt;= words[i].length &lt;= 12</code></li>
	<li><code>words[i]</code> 由小写英文字母组成</li>
</ul>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/unique-morse-code-words/description/)  -  [LeetCode-CN](https://leetcode.cn/problems/unique-morse-code-words/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| typescript  | 72 ms | 43.6 MB | 2022/04/10 22:06 |

```typescript

function uniqueMorseRepresentations(words: string[]): number {
  const hash = [".-","-...","-.-.","-..",".","..-.","--.","....","..",".---","-.-",".-..","--","-.","---",".--.","--.-",".-.","...","-","..-","...-",".--","-..-","-.--","--.."];

  const translated = words.map(w => w.split('').map(l => hash[l.codePointAt(0) - 'a'.codePointAt(0)]).join(''));

  return [...new Set(translated)].length;

};

```
## My Notes - 我的笔记


No notes

