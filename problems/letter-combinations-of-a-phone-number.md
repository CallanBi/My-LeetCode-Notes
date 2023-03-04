
# 17. Letter Combinations of a Phone Number - 电话号码的字母组合

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Hash Table-哈希表-blue.svg">   <img src="https://img.shields.io/badge/String-字符串-blue.svg">   <img src="https://img.shields.io/badge/Backtracking-回溯-blue.svg">  


## Description - 题目描述

### EN:
<p>Given a string containing digits from <code>2-9</code> inclusive, return all possible letter combinations that the number could represent. Return the answer in <strong>any order</strong>.</p>

<p>A mapping of digits to letters (just like on the telephone buttons) is given below. Note that 1 does not map to any letters.</p>
<img alt="" src="https://assets.leetcode.com/uploads/2022/03/15/1200px-telephone-keypad2svg.png" style="width: 300px; height: 243px;" />
<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input:</strong> digits = &quot;23&quot;
<strong>Output:</strong> [&quot;ad&quot;,&quot;ae&quot;,&quot;af&quot;,&quot;bd&quot;,&quot;be&quot;,&quot;bf&quot;,&quot;cd&quot;,&quot;ce&quot;,&quot;cf&quot;]
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre>
<strong>Input:</strong> digits = &quot;&quot;
<strong>Output:</strong> []
</pre>

<p><strong class="example">Example 3:</strong></p>

<pre>
<strong>Input:</strong> digits = &quot;2&quot;
<strong>Output:</strong> [&quot;a&quot;,&quot;b&quot;,&quot;c&quot;]
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>0 &lt;= digits.length &lt;= 4</code></li>
	<li><code>digits[i]</code> is a digit in the range <code>[&#39;2&#39;, &#39;9&#39;]</code>.</li>
</ul>


### ZH-CN:
<p>给定一个仅包含数字&nbsp;<code>2-9</code>&nbsp;的字符串，返回所有它能表示的字母组合。答案可以按 <strong>任意顺序</strong> 返回。</p>

<p>给出数字到字母的映射如下（与电话按键相同）。注意 1 不对应任何字母。</p>

<p><img src="https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2021/11/09/200px-telephone-keypad2svg.png" style="width: 200px;" /></p>

<p>&nbsp;</p>

<p><strong>示例 1：</strong></p>

<pre>
<strong>输入：</strong>digits = "23"
<strong>输出：</strong>["ad","ae","af","bd","be","bf","cd","ce","cf"]
</pre>

<p><strong>示例 2：</strong></p>

<pre>
<strong>输入：</strong>digits = ""
<strong>输出：</strong>[]
</pre>

<p><strong>示例 3：</strong></p>

<pre>
<strong>输入：</strong>digits = "2"
<strong>输出：</strong>["a","b","c"]
</pre>

<p>&nbsp;</p>

<p><strong>提示：</strong></p>

<ul>
	<li><code>0 &lt;= digits.length &lt;= 4</code></li>
	<li><code>digits[i]</code> 是范围 <code>['2', '9']</code> 的一个数字。</li>
</ul>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/letter-combinations-of-a-phone-number/description/)  -  [LeetCode-CN](https://leetcode.cn/problems/letter-combinations-of-a-phone-number/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| typescript  | 64 ms | 43.8 MB | 2022/05/01 23:52 |

```typescript

function letterCombinations(digits: string): string[] {
  if (digits === '') {
    return [];
  }

  const map = ['abc', 'def', 'ghi', 'jkl', 'mno', 'pqrs', 'tuv', 'wxyz'];

  const digitsArr = digits.split('');

  return digitsArr.reduce((acc: string[], cur, idx) => {
    const combine = map[parseInt(cur) - 2].split('');

    if (idx === 0) {
      return [...combine];
    }
    
    return acc.reduce((innerAcc, innerCur) => {
      return [...innerAcc, ...combine.map(i => {
        return `${innerCur}${i}`;
      })];
    }, [])
  }, []);


};

```
## My Notes - 我的笔记


reduce 套 reduce 搞定：

```typescript
function letterCombinations(digits: string): string[] {
  if (digits === '') {
    return [];
  }

  const map = ['abc', 'def', 'ghi', 'jkl', 'mno', 'pqrs', 'tuv', 'wxyz'];

  const digitsArr = digits.split('');

  return digitsArr.reduce((acc: string[], cur, idx) => {
    const combine = map[parseInt(cur) - 2].split('');

    if (idx === 0) {
      return [...combine];
    }
    
    return acc.reduce((innerAcc, innerCur) => {
      return [...innerAcc, ...combine.map(i => {
        return `${innerCur}${i}`;
      })];
    }, [])
  }, []);


};
```

