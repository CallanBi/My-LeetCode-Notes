
# 394. Decode String - 字符串解码

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Stack-栈-blue.svg">   <img src="https://img.shields.io/badge/Recursion-递归-blue.svg">   <img src="https://img.shields.io/badge/String-字符串-blue.svg">  


## Description - 题目描述

### EN:
<p>Given an encoded string, return its decoded string.</p>

<p>The encoding rule is: <code>k[encoded_string]</code>, where the <code>encoded_string</code> inside the square brackets is being repeated exactly <code>k</code> times. Note that <code>k</code> is guaranteed to be a positive integer.</p>

<p>You may assume that the input string is always valid; there are no extra white spaces, square brackets are well-formed, etc. Furthermore, you may assume that the original data does not contain any digits and that digits are only for those repeat numbers, <code>k</code>. For example, there will not be input like <code>3a</code> or <code>2[4]</code>.</p>

<p>The test cases are generated so that the length of the output will never exceed <code>10<sup>5</sup></code>.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input:</strong> s = &quot;3[a]2[bc]&quot;
<strong>Output:</strong> &quot;aaabcbc&quot;
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre>
<strong>Input:</strong> s = &quot;3[a2[c]]&quot;
<strong>Output:</strong> &quot;accaccacc&quot;
</pre>

<p><strong class="example">Example 3:</strong></p>

<pre>
<strong>Input:</strong> s = &quot;2[abc]3[cd]ef&quot;
<strong>Output:</strong> &quot;abcabccdcdcdef&quot;
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= s.length &lt;= 30</code></li>
	<li><code>s</code> consists of lowercase English letters, digits, and square brackets <code>&#39;[]&#39;</code>.</li>
	<li><code>s</code> is guaranteed to be <strong>a valid</strong> input.</li>
	<li>All the integers in <code>s</code> are in the range <code>[1, 300]</code>.</li>
</ul>


### ZH-CN:
<p>给定一个经过编码的字符串，返回它解码后的字符串。</p>

<p>编码规则为: <code>k[encoded_string]</code>，表示其中方括号内部的 <code>encoded_string</code> 正好重复 <code>k</code> 次。注意 <code>k</code> 保证为正整数。</p>

<p>你可以认为输入字符串总是有效的；输入字符串中没有额外的空格，且输入的方括号总是符合格式要求的。</p>

<p>此外，你可以认为原始数据不包含数字，所有的数字只表示重复的次数 <code>k</code> ，例如不会出现像&nbsp;<code>3a</code>&nbsp;或&nbsp;<code>2[4]</code>&nbsp;的输入。</p>

<p>&nbsp;</p>

<p><strong>示例 1：</strong></p>

<pre>
<strong>输入：</strong>s = "3[a]2[bc]"
<strong>输出：</strong>"aaabcbc"
</pre>

<p><strong>示例 2：</strong></p>

<pre>
<strong>输入：</strong>s = "3[a2[c]]"
<strong>输出：</strong>"accaccacc"
</pre>

<p><strong>示例 3：</strong></p>

<pre>
<strong>输入：</strong>s = "2[abc]3[cd]ef"
<strong>输出：</strong>"abcabccdcdcdef"
</pre>

<p><strong>示例 4：</strong></p>

<pre>
<strong>输入：</strong>s = "abc3[cd]xyz"
<strong>输出：</strong>"abccdcdcdxyz"
</pre>

<p>&nbsp;</p>

<p><strong>提示：</strong></p>

<ul>
	<li><code>1 &lt;= s.length &lt;= 30</code></li>
	<li><meta charset="UTF-8" /><code>s</code>&nbsp;由小写英文字母、数字和方括号<meta charset="UTF-8" />&nbsp;<code>'[]'</code> 组成</li>
	<li><code>s</code>&nbsp;保证是一个&nbsp;<strong>有效</strong>&nbsp;的输入。</li>
	<li><code>s</code>&nbsp;中所有整数的取值范围为<meta charset="UTF-8" />&nbsp;<code>[1, 300]</code>&nbsp;</li>
</ul>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/decode-string/description/)  -  [LeetCode-CN](https://leetcode.cn/problems/decode-string/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| python3  | 36 ms | 14.9 MB | 2023/04/09 18:41 |

```python3

class Solution:
  def decodeString(self, s: str) -> str:
    stack = []
    for c in s:
        if c != ']':
            stack.append(c)
        else:
            # Pop characters from the stack until the opening bracket is found
            temp_str = ""
            while stack and stack[-1] != '[':
                temp_str = stack.pop() + temp_str
            stack.pop()  # Remove the opening bracket

            # Find the number before the opening bracket and remove it from the stack
            k = ""
            while stack and stack[-1].isdigit():
                k = stack.pop() + k
            k = int(k)

            # Push the decoded substring back into the stack
            stack.append(temp_str * k)

    return "".join(stack)

```
## My Notes - 我的笔记


思路：用栈。
这是刚开始写的思路：栈中只存放左右括号，需要递归以及添加一堆条件判断。
```typescript
function decodeString(s: string): string {
  const parse = (start: number, end: number) => {
    let str = '';
    let counter = 0;
    const stack: string[] = [];
    let i = start;
    let leftIdx = -1;
    while (i <= end) {
      if (isNaN(Number(s[i]))) {
        if (s[i] !== '[' && s[i] !== ']') {
          if (stack.length === 0) {
            str += s[i];
          }
        } else {
          if (s[i] === '[') {
            if (stack.length === 0) {
              leftIdx = i;
            }
            stack.push(s[i]);
          } else {
            stack.pop();
            if (stack.length === 0) {
              const subStr = parse(leftIdx + 1, i - 1);
              for (let c = 0; c < counter; c++) {
                str += subStr;
              }
              leftIdx = -1;
            }
          }
        }
      } else {
        const numStart = i;
        while (!isNaN(Number(s[i]))) {
          i++;
        }
        if (stack.length === 0) {
          counter = parseInt(s.slice(numStart, i));
        }
        continue;
      }
      i++;
    }
    return str;
  }

  return parse(0, s.length - 1);
};
```
后来和同学交流后，发现其实可以把除了非右括号的所有东西都压入栈，更简单，而且不用递归：
```python
class Solution:
  def decodeString(self, s: str) -> str:
    stack = []
    for c in s:
        if c != ']':
            stack.append(c)
        else:
            # Pop characters from the stack until the opening bracket is found
            temp_str = ""
            while stack and stack[-1] != '[':
                temp_str = stack.pop() + temp_str
            stack.pop()  # Remove the opening bracket

            # Find the number before the opening bracket and remove it from the stack
            k = ""
            while stack and stack[-1].isdigit():
                k = stack.pop() + k
            k = int(k)

            # Push the decoded substring back into the stack
            stack.append(temp_str * k)

    return "".join(stack)
```

