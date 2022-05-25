
# 剑指 Offer 19. 正则表达式匹配 LCOF - 正则表达式匹配

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Recursion-递归-blue.svg">   <img src="https://img.shields.io/badge/String-字符串-blue.svg">   <img src="https://img.shields.io/badge/Dynamic Programming-动态规划-blue.svg">  


## Description - 题目描述

### EN:
English description is not available for the problem. Please switch to Chinese.

### ZH-CN:
<p>请实现一个函数用来匹配包含<code>&#39;. &#39;</code>和<code>&#39;*&#39;</code>的正则表达式。模式中的字符<code>&#39;.&#39;</code>表示任意一个字符，而<code>&#39;*&#39;</code>表示它前面的字符可以出现任意次（含0次）。在本题中，匹配是指字符串的所有字符匹配整个模式。例如，字符串<code>&quot;aaa&quot;</code>与模式<code>&quot;a.a&quot;</code>和<code>&quot;ab*ac*a&quot;</code>匹配，但与<code>&quot;aa.a&quot;</code>和<code>&quot;ab*a&quot;</code>均不匹配。</p>

<p><strong>示例 1:</strong></p>

<pre><strong>输入:</strong>
s = &quot;aa&quot;
p = &quot;a&quot;
<strong>输出:</strong> false
<strong>解释:</strong> &quot;a&quot; 无法匹配 &quot;aa&quot; 整个字符串。
</pre>

<p><strong>示例 2:</strong></p>

<pre><strong>输入:</strong>
s = &quot;aa&quot;
p = &quot;a*&quot;
<strong>输出:</strong> true
<strong>解释:</strong>&nbsp;因为 &#39;*&#39; 代表可以匹配零个或多个前面的那一个元素, 在这里前面的元素就是 &#39;a&#39;。因此，字符串 &quot;aa&quot; 可被视为 &#39;a&#39; 重复了一次。
</pre>

<p><strong>示例&nbsp;3:</strong></p>

<pre><strong>输入:</strong>
s = &quot;ab&quot;
p = &quot;.*&quot;
<strong>输出:</strong> true
<strong>解释:</strong>&nbsp;&quot;.*&quot; 表示可匹配零个或多个（&#39;*&#39;）任意字符（&#39;.&#39;）。
</pre>

<p><strong>示例 4:</strong></p>

<pre><strong>输入:</strong>
s = &quot;aab&quot;
p = &quot;c*a*b&quot;
<strong>输出:</strong> true
<strong>解释:</strong>&nbsp;因为 &#39;*&#39; 表示零个或多个，这里 &#39;c&#39; 为 0 个, &#39;a&#39; 被重复一次。因此可以匹配字符串 &quot;aab&quot;。
</pre>

<p><strong>示例 5:</strong></p>

<pre><strong>输入:</strong>
s = &quot;mississippi&quot;
p = &quot;mis*is*p*.&quot;
<strong>输出:</strong> false</pre>

<ul>
	<li><code>s</code>&nbsp;可能为空，且只包含从&nbsp;<code>a-z</code>&nbsp;的小写字母。</li>
	<li><code>p</code>&nbsp;可能为空，且只包含从&nbsp;<code>a-z</code>&nbsp;的小写字母以及字符&nbsp;<code>.</code>&nbsp;和&nbsp;<code>*</code>，无连续的 <code>&#39;*&#39;</code>。</li>
</ul>

<p>注意：本题与主站 10&nbsp;题相同：<a href="https://leetcode-cn.com/problems/regular-expression-matching/">https://leetcode-cn.com/problems/regular-expression-matching/</a></p>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/zheng-ze-biao-da-shi-pi-pei-lcof/description/)  -  [LeetCode-CN](https://leetcode.cn/problems/zheng-ze-biao-da-shi-pi-pei-lcof/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| typescript  | 80 ms | 46.9 MB | 2022/04/30 23:18 |

```typescript

function isMatch(s: string, p: string): boolean {
  const m = s.length + 1, n = p.length + 1;
  const dp: boolean[][] = new Array(m).fill(false).map(i => new Array(n).fill(false));
  dp[0][0] = true;
  for (let j = 2; j < n; j += 2)
  dp[0][j] = dp[0][j - 2] && p[j - 1] === '*';
  for (let i = 1; i < m; i++) {
    for (let j = 1; j < n; j++) {
      dp[i][j] = p[j - 1] === '*' ?
        dp[i][j - 2] || dp[i - 1][j] && (s[i - 1] === p[j - 2] || p[j - 2] === '.') :
        dp[i - 1][j - 1] && (p[j - 1] === '.' || s[i - 1] === p[j - 1]);
    }
  }
  return dp[m - 1][n - 1];

};

```
## My Notes - 我的笔记


# 直接用正则的作弊方法：

```typescript
function isMatch(s: string, p: string): boolean {
  return new RegExp(`^${p}$`).test(s)
};
```

# 剑指 offer 上原本的递归方法：

```typescript
function isMatch(s: string, p: string): boolean {
 return isMatchIdx(s, p, 0, 0);
};

function isMatchIdx(s: string, p: string, sIdx: number, pIdx: number): boolean {
 if(!s[sIdx] && !p[pIdx]) {
   return true;
 }

 if (s[sIdx] && !p[pIdx]) {
   return false;
 }

 if (p[pIdx+1] === '*') {
   if (s[sIdx] === p[pIdx] || (p[pIdx] === '.' && s[sIdx])) { // s 不能为空的原因： '.'正则要求必须至少有一个字符
     return isMatchIdx(s, p, sIdx+1, pIdx+2) // 例子：s === 'dbc', p === 'a*bc'
     || isMatchIdx(s, p, sIdx+1, pIdx) // 例子：s === 'aaabc', p === 'a*bc'
     || isMatchIdx(s, p, sIdx, pIdx+2); // 例子： s === 'abc', p === 'a*abc'
   } else {
     return isMatchIdx(s, p, sIdx, pIdx+2); // 例子： s === 'bc', p === 'a*bc'
   }
 }

 if (s[sIdx] === p[pIdx] || (p[pIdx] === '.' && s[sIdx])) {
   return isMatchIdx(s, p, sIdx+1, pIdx+1); // 若第一个字符匹配上，则模式和字符串比较位置向后移一位
 }

 return false;
}
```

# 终极方法：使用动态规划

```typescript
function isMatch(s: string, p: string): boolean {
  const sLen = s.length;
  const pLen = p.length;
  const dp = new Array<boolean[]>(sLen+1);
  for (let idx = 0; idx < dp.length; idx++) {
    dp[idx] = new Array<boolean>(pLen+1).fill(false);
  }

  const isMatchIdx: (sIdx: number, pIdx: number) => boolean = (sIdx, pIdx) => {
    return p[pIdx-2] === s[sIdx-1] || p[pIdx-2] === '.';
  }

  // 初始化 dp
  dp[0][0] = true;
  for(let j = 2; j <= pLen; j += 2) {
    //当s为空时，p必须满足a*b*.*这样的结构才能匹配成空串
    //当s不为空，p为空为false
    dp[0][j] = dp[0][j - 2] && p[j - 1] == '*';
  }

  for (let i = 1; i < sLen+1; i++) {
    for (let j = 0; j < pLen+1; j++) {
      if (p[j-1] === '*') {
        if (isMatchIdx(i, j)) {
          dp[i][j] = dp[i][j-2] || dp[i-1][j];
        } else {
          dp[i][j] = dp[i][j-2];
        }
      } else {
        if (isMatchIdx(i, j+1)) {
          dp[i][j] = dp[i-1][j-1];
        } else {
          dp[i][j] =false;
        }
      }
    }
  }

  return dp[sLen][pLen];
};
```

## 详解：

本方法主要参考了：[Krahets 的题解](https://leetcode-cn.com/problems/zheng-ze-biao-da-shi-pi-pei-lcof/solution/jian-zhi-offer-19-zheng-ze-biao-da-shi-pi-pei-dong/)

个人认为，动态规划的好处是不用考虑太多边界条件。只要状态转移方程考虑得比较全面，一维动态规划，最少只需初始化首个数，二维动态规划，最少只需初始化第一行。上述二维动态规划即是用了初始化一行的方法。

1.  设 `dp[i][j]` 为指针指在 s 的第 i 个和 p 的第 j 个字符时的结果，即 `s[i-1]` 和 `p[j-1]` 匹配的结果。接下来的解题过程要十分注意循环和`s, p`字符串的下标。

上述状态转移方程我用在打草稿时列了类似下式：

$$
while \ p[j-1] = *,  \ then:   \\
    dp[i][j] = dp[i-1][j] \ or \ dp[i][j-2], \ \ \  p[j-2] = s[i-1]  \ or \ p[j-2] = .  \ \ \ \  otherwise\\
	dp[i][j] = dp[i][j-2] \\
	while \ p[j-1] \neq *,  \ then:   \\
		dp[i][j] = dp[i-1][j-1], \ \ \ p[j-1] = s[i-1] \ or \  p[j-1] = .  \ \ \ \  otherwise\\
	dp[i][j] = false  \\
$$

初始化`dp[0][0] = true`，即字符串和模式都为空时是对的。

初始化第一行的原因已经在注释列出，具体可参考[Krahets 的题解](https://leetcode-cn.com/problems/zheng-ze-biao-da-shi-pi-pei-lcof/solution/jian-zhi-offer-19-zheng-ze-biao-da-shi-pi-pei-dong/)

注意：由于 `dp[i][j]` 为指针指在 s 的第 i 个和 p 的第 j 个字符时的结果，所以整个 dp 的大小是 `(sLen+1) *(pLen+1)` ,下标为 0 时代表`s`, `p` 各自的空字符串。此时在双循环 `dp` 时，注意边界是 `sLen +1` 和 `pLen + 1`。

`isMatchIdx()`是设置为判断 $  p[j-2] = s[i-1] \ or \  p[j-2] = . $ 的辅助函数，所以在判断 $p[j-1] = s[i-1] \ or \  p[j-1] = .$ 时，需要调用 `isMatchIdx(i, j+1)`。编写时需要格外注意下标。


