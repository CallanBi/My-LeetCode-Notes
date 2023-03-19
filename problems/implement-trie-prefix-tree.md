
# 208. Implement Trie (Prefix Tree) - 实现 Trie (前缀树)

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Design-设计-blue.svg">   <img src="https://img.shields.io/badge/Trie-字典树-blue.svg">   <img src="https://img.shields.io/badge/Hash Table-哈希表-blue.svg">   <img src="https://img.shields.io/badge/String-字符串-blue.svg">  


## Description - 题目描述

### EN:
<p>A <a href="https://en.wikipedia.org/wiki/Trie" target="_blank"><strong>trie</strong></a> (pronounced as &quot;try&quot;) or <strong>prefix tree</strong> is a tree data structure used to efficiently store and retrieve keys in a dataset of strings. There are various applications of this data structure, such as autocomplete and spellchecker.</p>

<p>Implement the Trie class:</p>

<ul>
	<li><code>Trie()</code> Initializes the trie object.</li>
	<li><code>void insert(String word)</code> Inserts the string <code>word</code> into the trie.</li>
	<li><code>boolean search(String word)</code> Returns <code>true</code> if the string <code>word</code> is in the trie (i.e., was inserted before), and <code>false</code> otherwise.</li>
	<li><code>boolean startsWith(String prefix)</code> Returns <code>true</code> if there is a previously inserted string <code>word</code> that has the prefix <code>prefix</code>, and <code>false</code> otherwise.</li>
</ul>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input</strong>
[&quot;Trie&quot;, &quot;insert&quot;, &quot;search&quot;, &quot;search&quot;, &quot;startsWith&quot;, &quot;insert&quot;, &quot;search&quot;]
[[], [&quot;apple&quot;], [&quot;apple&quot;], [&quot;app&quot;], [&quot;app&quot;], [&quot;app&quot;], [&quot;app&quot;]]
<strong>Output</strong>
[null, null, true, false, true, null, true]

<strong>Explanation</strong>
Trie trie = new Trie();
trie.insert(&quot;apple&quot;);
trie.search(&quot;apple&quot;);   // return True
trie.search(&quot;app&quot;);     // return False
trie.startsWith(&quot;app&quot;); // return True
trie.insert(&quot;app&quot;);
trie.search(&quot;app&quot;);     // return True
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= word.length, prefix.length &lt;= 2000</code></li>
	<li><code>word</code> and <code>prefix</code> consist only of lowercase English letters.</li>
	<li>At most <code>3 * 10<sup>4</sup></code> calls <strong>in total</strong> will be made to <code>insert</code>, <code>search</code>, and <code>startsWith</code>.</li>
</ul>


### ZH-CN:
<p><strong><a href="https://baike.baidu.com/item/字典树/9825209?fr=aladdin" target="_blank">Trie</a></strong>（发音类似 "try"）或者说 <strong>前缀树</strong> 是一种树形数据结构，用于高效地存储和检索字符串数据集中的键。这一数据结构有相当多的应用情景，例如自动补完和拼写检查。</p>

<p>请你实现 Trie 类：</p>

<ul>
	<li><code>Trie()</code> 初始化前缀树对象。</li>
	<li><code>void insert(String word)</code> 向前缀树中插入字符串 <code>word</code> 。</li>
	<li><code>boolean search(String word)</code> 如果字符串 <code>word</code> 在前缀树中，返回 <code>true</code>（即，在检索之前已经插入）；否则，返回 <code>false</code> 。</li>
	<li><code>boolean startsWith(String prefix)</code> 如果之前已经插入的字符串 <code>word</code> 的前缀之一为 <code>prefix</code> ，返回 <code>true</code> ；否则，返回 <code>false</code> 。</li>
</ul>

<p> </p>

<p><strong>示例：</strong></p>

<pre>
<strong>输入</strong>
["Trie", "insert", "search", "search", "startsWith", "insert", "search"]
[[], ["apple"], ["apple"], ["app"], ["app"], ["app"], ["app"]]
<strong>输出</strong>
[null, null, true, false, true, null, true]

<strong>解释</strong>
Trie trie = new Trie();
trie.insert("apple");
trie.search("apple");   // 返回 True
trie.search("app");     // 返回 False
trie.startsWith("app"); // 返回 True
trie.insert("app");
trie.search("app");     // 返回 True
</pre>

<p> </p>

<p><strong>提示：</strong></p>

<ul>
	<li><code>1 <= word.length, prefix.length <= 2000</code></li>
	<li><code>word</code> 和 <code>prefix</code> 仅由小写英文字母组成</li>
	<li><code>insert</code>、<code>search</code> 和 <code>startsWith</code> 调用次数 <strong>总计</strong> 不超过 <code>3 * 10<sup>4</sup></code> 次</li>
</ul>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/implement-trie-prefix-tree/description/)  -  [LeetCode-CN](https://leetcode.cn/problems/implement-trie-prefix-tree/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| typescript  | 188 ms | 64.8 MB | 2023/03/19 11:12 |

```typescript

class Trie {
  private _children: Trie[];
  private _isEnd: boolean;

  constructor() {
    this._children = new Array(26).fill(null);
    this._isEnd = false;
  }

  insert(word: string): void {
    let cur: Trie = this;
    for (const w of word) {
      const idx = w.charCodeAt(0) - 'a'.charCodeAt(0);
      if (!cur._children[idx]) {
        cur._children[idx] = new Trie();
      }
      cur = cur._children[idx];
    }
    cur._isEnd = true;
  }

  search(word: string): boolean {
    let cur: Trie = this;
    for (const w of word) {
      const idx = w.charCodeAt(0) - 'a'.charCodeAt(0);
      if (cur._children[idx]) {
        cur = cur._children[idx];
      } else {
        return false;
      }
    }
    return cur._isEnd;
  }

  startsWith(prefix: string): boolean {
    let cur: Trie = this;
    for (const w of prefix) {
      const idx = w.charCodeAt(0) - 'a'.charCodeAt(0);
      if (cur._children[idx]) {
        cur = cur._children[idx];
      } else {
        return false;
      }
    }
    return true;
  }
}

/**
 * Your Trie object will be instantiated and called as such:
 * var obj = new Trie()
 * obj.insert(word)
 * var param_2 = obj.search(word)
 * var param_3 = obj.startsWith(prefix)
 */

```
## My Notes - 我的笔记


根据[官方题解](https://leetcode.cn/problems/implement-trie-prefix-tree/solutions/)理解了字典树之后写的代码：
```typescript
class Trie {
  private _children: Trie[];
  private _isEnd: boolean;

  constructor() {
    this._children = new Array(26).fill(null);
    this._isEnd = false;
  }

  insert(word: string): void {
    let cur: Trie = this;
    for (const w of word) {
      const idx = w.charCodeAt(0) - 'a'.charCodeAt(0);
      if (!cur._children[idx]) {
        cur._children[idx] = new Trie();
      }
      cur = cur._children[idx];
    }
    cur._isEnd = true;
  }

  search(word: string): boolean {
    let cur: Trie = this;
    for (const w of word) {
      const idx = w.charCodeAt(0) - 'a'.charCodeAt(0);
      if (cur._children[idx]) {
        cur = cur._children[idx];
      } else {
        return false;
      }
    }
    return cur._isEnd;
  }

  startsWith(prefix: string): boolean {
    let cur: Trie = this;
    for (const w of prefix) {
      const idx = w.charCodeAt(0) - 'a'.charCodeAt(0);
      if (cur._children[idx]) {
        cur = cur._children[idx];
      } else {
        return false;
      }
    }
    return true;
  }
}

/**
 * Your Trie object will be instantiated and called as such:
 * var obj = new Trie()
 * obj.insert(word)
 * var param_2 = obj.search(word)
 * var param_3 = obj.startsWith(prefix)
 */
```

