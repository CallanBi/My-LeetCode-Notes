
# 5. Longest Palindromic Substring - 最长回文子串

## Tags - 题目标签

 <img src="https://img.shields.io/badge/String-字符串-blue.svg">   <img src="https://img.shields.io/badge/Dynamic Programming-动态规划-blue.svg">  


## Description - 题目描述

### EN:
<p>Given a string <code>s</code>, return <em>the longest palindromic substring</em> in <code>s</code>.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>

<pre>
<strong>Input:</strong> s = &quot;babad&quot;
<strong>Output:</strong> &quot;bab&quot;
<strong>Explanation:</strong> &quot;aba&quot; is also a valid answer.
</pre>

<p><strong>Example 2:</strong></p>

<pre>
<strong>Input:</strong> s = &quot;cbbd&quot;
<strong>Output:</strong> &quot;bb&quot;
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= s.length &lt;= 1000</code></li>
	<li><code>s</code> consist of only digits and English letters.</li>
</ul>


### ZH-CN:
<p>给你一个字符串 <code>s</code>，找到 <code>s</code> 中最长的回文子串。</p>

<p>&nbsp;</p>

<p><strong>示例 1：</strong></p>

<pre>
<strong>输入：</strong>s = "babad"
<strong>输出：</strong>"bab"
<strong>解释：</strong>"aba" 同样是符合题意的答案。
</pre>

<p><strong>示例 2：</strong></p>

<pre>
<strong>输入：</strong>s = "cbbd"
<strong>输出：</strong>"bb"
</pre>

<p>&nbsp;</p>

<p><strong>提示：</strong></p>

<ul>
	<li><code>1 &lt;= s.length &lt;= 1000</code></li>
	<li><code>s</code> 仅由数字和英文字母组成</li>
</ul>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/longest-palindromic-substring/description/)  -  [LeetCode-CN](https://leetcode.cn/problems/longest-palindromic-substring/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| javascript  | 304 ms | N/A | 2018/11/17 16:15 |

```javascript

/**
 * @param {string} s
 * @return {string}
 */

var longestPalindrome = function(s) {
    if(s === null || s.length <=1 ){
       return s ;
    }
    const len = s.length;
    var boolTable = new Array(len);
    for (var i = 0; i < len; i++) {
        boolTable[i] = new Array(len);
    }
    
    for (i=0;i<len;i++) {
        boolTable[i][i] = true;
    }
    for (i=0;i<len-1;i++) {
        boolTable[i+1][i] = s.charAt(i)===s.charAt(i+1);
    }
    
    for (var j=0;j<len;j++) {
        for(i=0;i<j;i++) {
            if(j-i>1) {
                boolTable[j][i] =  boolTable[j-1][i+1] && s.charAt(i) === s.charAt(j);
            }
        }
    }
    
    var ansI = -1,
        ansJ = -1,
        maxLength = -1;
    
    for (j=0;j<len;j++) {
        for (i=0;i<=j;i++) {
            if (boolTable[j][i] && j-i>=maxLength) {
                ansI = i;
                ansJ = j;
                maxLength = j-i;
            }
        }
    }
    return s.slice(ansI,ansJ+1);
}

```
## My Notes - 我的笔记


# 思路：

## 反转字符串，比较下同一正序和反序索引一样的字符即可

## 动态规划

设`dp[i][j]` 为以 $[ i, j )$ 为 范围截取 `s` 时的子串是否是回文。

递推式为:

$dp[i-1][j+1] = true, \qquad dp[i][j] = true \quad and \quad s[i] = s[j-1]$

$otherwize \qquad dp[i-1][j+1] = false$


## 5 最长回文子串

### 方法一 暴力法

暴力法将选出所有子字符串可能的开始和结束位置，并检验它是不是回文。

```javascript
function reverse(str){
    return str.split('').reverse().join('');
};

var longestPalindrome = function(s) {
    if (s) {
        var len = s.length,
            ansArray = [],
            max = -1,
            maxIndex = -1,
            temp = "",
            tempReversed = "";
        for (var i = 0; i < len; i++) {
            for (var j = i; j < len; j++) {
                temp = s.slice(i, j+1);
                tempReversed = reverse(temp);
               if (temp === tempReversed && temp.length >= max) {
                    ansArray.push(temp);
                   max = temp.length;
                }
           }
        }
        return ansArray[ansArray.length-1];
    } else {
        return "";
    }
};
```

时间复杂度：O(n^3)


### 方法二 倒序法(最长公共子串)

**常见错误**

有些人会忍不住提出一个快速的解决方案，不幸的是，这个解决方案有缺陷(但是可以很容易地纠正)：

> 反转 SS，使之变成 S&#x27;S′。找到 SS 和 S&#x27;S′ 之间最长的公共子串，这也必然是最长的回文子串。

这似乎是可行的，让我们看看下面的一些例子。

例如，S=“caba” , S′=“abac”：

S 以及 S‘ 之间的最长公共子串为 “aba”，恰恰是答案。

让我们尝试一下这个例子：S = “abacdfgdcaba“ , S′=“abacdgfdcaba”：

S 以及 S′ 之间的最长公共子串为 “abacd”，显然，这不是回文。

**算法**

我们可以看到，当 SS 的其他部分中存在非回文子串的反向副本时，最长公共子串法就会失败。为了纠正这一点，每当我们找到最长的公共子串的候选项时，都需要检查子串的索引是否与反向子串的原始索引相同。如果相同，那么我们尝试更新目前为止找到的最长回文子串；如果不是，我们就跳过这个候选项并继续寻找下一个候选。

```javascript
function reverse(str){
    return str.split('').reverse().join('');
};

var longestPalindrome = function(s) {
    if (s) {
        var commonString = [],
        sReversed = reverse(s),
        len = s.length,
        max = -1,
        maxIndex = -1,
        temp = "";
    
        for (var i = 0; i < len; i++) {
            for (var j = i; j < len; j++) {
                temp = s.slice(i, j+1);
                if(sReversed.indexOf(temp) >= 0 && sReversed.indexOf(temp) === len-j-1 && temp.length >= max) {
                    commonString.push(temp); 
                    max = temp.length;
                }
            }
        }
        return commonString[commonString.length-1];
    } else {
        return "";
    }
};
```

时间按复杂度：O(n^2)


### 方法三 动态规划

为了改进暴力法，我们首先观察如何避免在验证回文时进行不必要的重复计算。考虑 “ababa” 这个示例。如果我们已经知道 “bab” 是回文，那么很明显，“ababa” 一定是回文，因为它的左首字母和右尾字母是相同的。

```javascript
/**
 * @param {string} s
 * @return {string}
 */

var longestPalindrome = function(s) {
    if(s === null || s.length <=1 ){
       return s ;
    }
    const len = s.length;
    var boolTable = new Array(len);
    for (var i = 0; i < len; i++) {
        boolTable[i] = new Array(len);
    }
    
    for (i=0;i<len;i++) {
        boolTable[i][i] = true;
    }
    for (i=0;i<len-1;i++) {
        boolTable[i+1][i] = s.charAt(i)===s.charAt(i+1);
    }
    
    for (var j=0;j<len;j++) {
        for(i=0;i<j;i++) {
            if(j-i>1) {
                boolTable[j][i] =  boolTable[j-1][i+1] && s.charAt(i) === s.charAt(j);
            }
        }
    }
    
    var ansI = -1,
        ansJ = -1,
        maxLength = -1;
    
    for (j=0;j<len;j++) {
        for (i=0;i<=j;i++) {
            if (boolTable[j][i] && j-i>=maxLength) {
                ansI = i;
                ansJ = j;
                maxLength = j-i;
            }
        }
    }
    return s.slice(ansI,ansJ+1);
}
```

时间复杂度：O(n^2)

