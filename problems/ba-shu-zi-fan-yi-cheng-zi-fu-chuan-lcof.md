
# 剑指 Offer 46. 把数字翻译成字符串 LCOF - 把数字翻译成字符串

## Tags - 题目标签

 <img src="https://img.shields.io/badge/String-字符串-blue.svg">   <img src="https://img.shields.io/badge/Dynamic Programming-动态规划-blue.svg">  


## Description - 题目描述

### EN:
English description is not available for the problem. Please switch to Chinese.

### ZH-CN:
<p>给定一个数字，我们按照如下规则把它翻译为字符串：0 翻译成 &ldquo;a&rdquo; ，1 翻译成 &ldquo;b&rdquo;，&hellip;&hellip;，11 翻译成 &ldquo;l&rdquo;，&hellip;&hellip;，25 翻译成 &ldquo;z&rdquo;。一个数字可能有多个翻译。请编程实现一个函数，用来计算一个数字有多少种不同的翻译方法。</p>

<p>&nbsp;</p>

<p><strong>示例 1:</strong></p>

<pre><strong>输入:</strong> 12258
<strong>输出:</strong> <code>5
</code><strong>解释:</strong> 12258有5种不同的翻译，分别是&quot;bccfi&quot;, &quot;bwfi&quot;, &quot;bczi&quot;, &quot;mcfi&quot;和&quot;mzi&quot;</pre>

<p>&nbsp;</p>

<p><strong>提示：</strong></p>

<ul>
	<li><code>0 &lt;= num &lt; 2<sup>31</sup></code></li>
</ul>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/ba-shu-zi-fan-yi-cheng-zi-fu-chuan-lcof/description/)  -  [LeetCode-CN](https://leetcode.cn/problems/ba-shu-zi-fan-yi-cheng-zi-fu-chuan-lcof/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| typescript  | 60 ms | 39.4 MB | 2021/12/18 14:57 |

```typescript

function translateNum(num: number): number {
  const dp: number[] = [];
  dp[0] = 1;
  const str = String(num);
  if (Number(str.slice(0, 2)) <= 25 && str.slice(0, 1) !== '0') {
    dp[1] = 2;
  } else {
    dp[1] = 1;
  }

  for (let i = 2; i < str.length; i++) {
    const subStr = str.slice(i-1, i+1);
    if (Number(subStr) <= 25 && subStr[0] !== '0') {
      dp[i] = dp[i-2] + dp[i-1];
    } else {
      dp[i] = dp[i-1];
    }
  }
  return dp[str.length-1];
};

```
## My Notes - 我的笔记


# 直观方法：递归
```typescript
function translateNum(num: number): number {
  return recur(String(num));
};

function recur(str: string): number {
  if (!str) {
    return 0;
  }
  if (str.length === 2 || str.length === 1) {
    if (str.length === 2 && Number(str) <= 25 && str[0] !== '0') {
      return 2;
    } else {
      return 1;
    }
  }
  if (Number(str.slice(0, 2)) <= 25 && str[0] !== '0') {
    return recur(str.slice(2)) + recur(str.slice(1));
  } else {
    return recur(str.slice(1));
  }
}
```

# 用动态规划优化：
设 `dp[n]` 为数字串从索引`0`到索引`n`（包括）的所有翻译情况。

如果` n - 1`位和` n `位组成的数字合法，那`n` 位可以单独构成数字，也可以和`n - 1`位组合在一起，所以从`0`到 `n` 位翻译情况是从`0`到 `n - 1`位翻译的所有情况和从`0`到`n - 2` 位的所有情况加起来。

如果` n - 1`位和` n `位组成的数字非法，那 `n` 位一定单独构成数字。所以从`0`到 `n` 位翻译情况是从`0`到 `n - 1`位翻译的所有情况。（注意：别搞成`dp[n-2]`，那是最后两位组合在一起的情况。）

```typescript
function translateNum(num: number): number {
  const dp: number[] = [];
  dp[0] = 1;
  const str = String(num);
  if (Number(str.slice(0, 2)) <= 25 && str.slice(0, 1) !== '0') {
    dp[1] = 2;
  } else {
    dp[1] = 1;
  }

  for (let i = 2; i < str.length; i++) {
    const subStr = str.slice(i-1, i+1);
    if (Number(subStr) <= 25 && subStr[0] !== '0') {
      dp[i] = dp[i-2] + dp[i-1];
    } else {
      dp[i] = dp[i-1];
    }
  }
  return dp[str.length-1];
};
```


