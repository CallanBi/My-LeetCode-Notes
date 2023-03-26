
# 301. Remove Invalid Parentheses - 删除无效的括号

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Breadth First Search-广度优先搜索-blue.svg">   <img src="https://img.shields.io/badge/String-字符串-blue.svg">   <img src="https://img.shields.io/badge/Backtracking-回溯-blue.svg">  


## Description - 题目描述

### EN:
<p>Given a string <code>s</code> that contains parentheses and letters, remove the minimum number of invalid parentheses to make the input string valid.</p>

<p>Return <em>a list of <strong>unique strings</strong> that are valid with the minimum number of removals</em>. You may return the answer in <strong>any order</strong>.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input:</strong> s = &quot;()())()&quot;
<strong>Output:</strong> [&quot;(())()&quot;,&quot;()()()&quot;]
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre>
<strong>Input:</strong> s = &quot;(a)())()&quot;
<strong>Output:</strong> [&quot;(a())()&quot;,&quot;(a)()()&quot;]
</pre>

<p><strong class="example">Example 3:</strong></p>

<pre>
<strong>Input:</strong> s = &quot;)(&quot;
<strong>Output:</strong> [&quot;&quot;]
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= s.length &lt;= 25</code></li>
	<li><code>s</code> consists of lowercase English letters and parentheses <code>&#39;(&#39;</code> and <code>&#39;)&#39;</code>.</li>
	<li>There will be at most <code>20</code> parentheses in <code>s</code>.</li>
</ul>


### ZH-CN:
<p>给你一个由若干括号和字母组成的字符串 <code>s</code> ，删除最小数量的无效括号，使得输入的字符串有效。</p>

<p>返回所有可能的结果。答案可以按 <strong>任意顺序</strong> 返回。</p>

<p> </p>

<p><strong>示例 1：</strong></p>

<pre>
<strong>输入：</strong>s = "()())()"
<strong>输出：</strong>["(())()","()()()"]
</pre>

<p><strong>示例 2：</strong></p>

<pre>
<strong>输入：</strong>s = "(a)())()"
<strong>输出：</strong>["(a())()","(a)()()"]
</pre>

<p><strong>示例 3：</strong></p>

<pre>
<strong>输入：</strong>s = ")("
<strong>输出：</strong>[""]
</pre>

<p> </p>

<p><strong>提示：</strong></p>

<ul>
	<li><code>1 <= s.length <= 25</code></li>
	<li><code>s</code> 由小写英文字母以及括号 <code>'('</code> 和 <code>')'</code> 组成</li>
	<li><code>s</code> 中至多含 <code>20</code> 个括号</li>
</ul>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/remove-invalid-parentheses/description/)  -  [LeetCode-CN](https://leetcode.cn/problems/remove-invalid-parentheses/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| typescript  | 84 ms | 44.6 MB | 2023/03/26 23:36 |

```typescript

function removeInvalidParentheses(s: string): string[] {
  const res = new Set<string>();

  let lremove = 0, rremove = 0;

  for (const c of s) {
    if (c === '(') {
      lremove++;
    } else if (c === ')') {
      if (lremove === 0) {
        rremove++;
      } else {
        lremove--;
      }
    }
  }

  if (lremove === 0 && rremove === 0) {
    return [s];
  }

  const isValid = (s: string) => {
    if (s === '') {
      return true;
    }

    let lcount = 0;
    for (const c of s) {
      if (c === '(') {
        lcount++;
      } else if (c === ')') {
        if (lcount === 0) {
          return false;
        } else {
          lcount--;
        }
      }
    }
    return true;
  }

  const dfs = (s: string, start: number, lremove: number, rremove: number) => {
    if (s.length < lremove + rremove) {
      return;
    }

    if (lremove === 0 && rremove === 0 && isValid(s)) {
      res.add(s);
      return;
    }

    for (let i = start; i < s.length; i++) {
      if (i !== start && s[i] === s[i - 1]) {
        continue;
      }
      if (s[i] === '(') {
        if (lremove > 0) {
          dfs(s.slice(0, i) + s.slice(i + 1), i, lremove - 1, rremove);
        }
      } else if (s[i] === ')') {
        if (rremove > 0) {
          dfs(s.slice(0, i) + s.slice(i + 1), i, lremove, rremove - 1);
        }
      }
    }
  }

  dfs(s, 0, lremove, rremove);

  return [...res];
};

```
## My Notes - 我的笔记


# dfs + 剪枝
建议先看官方题解再看这个笔记。

刚开始用 dfs + 剪枝，超时：
```typescript
function removeInvalidParentheses(s: string): string[] {
  const res = new Set<string>();

  let lremove = 0, rremove = 0;

  for (const c of s) {
    if (c === '(') {
      lremove++;
    } else if (c === ')') {
      if (lremove === 0) {
        rremove++;
      } else {
        lremove--;
      }
    }
  }

  if (lremove === 0 && rremove === 0) {
    return [s];
  }

  const isValid = (s: string) => {
    if (s === '') {
      return true;
    }

    let lcount = 0;
    for (const c of s) {
      if (c === '(') {
        lcount++;
      } else if (c === ')') {
        if (lcount === 0) {
          return false;
        } else {
          lcount--;
        }
      }
    }
    return true;
  }

  const dfs = (s: string, lremove: number, rremove: number) => {
    if (s.length < lremove + rremove) {
      return;
    }

    if (lremove === 0 && rremove === 0 && isValid(s)) {
      res.add(s);
      return;
    }

    for (let i = 0; i < s.length; i++) {
      if (s[i] === '(') {
        if (lremove > 0) {
          dfs(s.slice(0, i) + s.slice(i + 1), lremove - 1, rremove);
        }
      } else if (s[i] === ')') {
        if (rremove > 0) {
          dfs(s.slice(0, i) + s.slice(i + 1), lremove, rremove - 1);
        }
      }
    }
  }

  dfs(s, lremove, rremove);

  return [...res];
};
```

应该是有一些需要剪枝的地方没剪。参照官方题解，应该在遍历字符串的dfs 中传入一个`start`位，即只从`start`的位置开始尝试删除括号（因为`start`前面已经删除过了），并且当连续遇到连续相同的括号时，跳过遍历（后面如果不合法必然会被剪枝掉），否则如果连续括号很多的话，时间复杂度非常高。

```typescript
function removeInvalidParentheses(s: string): string[] {
  const res = new Set<string>();

  let lremove = 0, rremove = 0;

  for (const c of s) {
    if (c === '(') {
      lremove++;
    } else if (c === ')') {
      if (lremove === 0) {
        rremove++;
      } else {
        lremove--;
      }
    }
  }

  if (lremove === 0 && rremove === 0) {
    return [s];
  }

  const isValid = (s: string) => {
    if (s === '') {
      return true;
    }

    let lcount = 0;
    for (const c of s) {
      if (c === '(') {
        lcount++;
      } else if (c === ')') {
        if (lcount === 0) {
          return false;
        } else {
          lcount--;
        }
      }
    }
    return true;
  }

  const dfs = (s: string, start: number, lremove: number, rremove: number) => {
    if (s.length < lremove + rremove) {
      return;
    }

    if (lremove === 0 && rremove === 0 && isValid(s)) {
      res.add(s);
      return;
    }

    for (let i = start; i < s.length; i++) {
      if (i !== start && s[i] === s[i - 1]) {
        continue;
      }
      if (s[i] === '(') {
        if (lremove > 0) {
          dfs(s.slice(0, i) + s.slice(i + 1), i, lremove - 1, rremove);
        }
      } else if (s[i] === ')') {
        if (rremove > 0) {
          dfs(s.slice(0, i) + s.slice(i + 1), i, lremove, rremove - 1);
        }
      }
    }
  }

  dfs(s, 0, lremove, rremove);

  return [...res];
};
```

