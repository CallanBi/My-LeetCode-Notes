
# 461. Hamming Distance - 汉明距离

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Bit Manipulation-位运算-blue.svg">  


## Description - 题目描述

### EN:
<p>The <a href="https://en.wikipedia.org/wiki/Hamming_distance" target="_blank">Hamming distance</a> between two integers is the number of positions at which the corresponding bits are different.</p>

<p>Given two integers <code>x</code> and <code>y</code>, return <em>the <strong>Hamming distance</strong> between them</em>.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input:</strong> x = 1, y = 4
<strong>Output:</strong> 2
<strong>Explanation:</strong>
1   (0 0 0 1)
4   (0 1 0 0)
       &uarr;   &uarr;
The above arrows point to positions where the corresponding bits are different.
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre>
<strong>Input:</strong> x = 3, y = 1
<strong>Output:</strong> 1
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>0 &lt;=&nbsp;x, y &lt;= 2<sup>31</sup> - 1</code></li>
</ul>


### ZH-CN:
<p>两个整数之间的 <a href="https://baike.baidu.com/item/%E6%B1%89%E6%98%8E%E8%B7%9D%E7%A6%BB">汉明距离</a> 指的是这两个数字对应二进制位不同的位置的数目。</p>

<p>给你两个整数 <code>x</code> 和 <code>y</code>，计算并返回它们之间的汉明距离。</p>

<p> </p>

<p><strong>示例 1：</strong></p>

<pre>
<strong>输入：</strong>x = 1, y = 4
<strong>输出：</strong>2
<strong>解释：</strong>
1   (0 0 0 1)
4   (0 1 0 0)
       ↑   ↑
上面的箭头指出了对应二进制位不同的位置。
</pre>

<p><strong>示例 2：</strong></p>

<pre>
<strong>输入：</strong>x = 3, y = 1
<strong>输出：</strong>1
</pre>

<p> </p>

<p><strong>提示：</strong></p>

<ul>
	<li><code>0 <= x, y <= 2<sup>31</sup> - 1</code></li>
</ul>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/hamming-distance/description/)  -  [LeetCode-CN](https://leetcode.cn/problems/hamming-distance/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| typescript  | 64 ms | 42.5 MB | 2023/07/23 13:15 |

```typescript

function hammingDistance(x: number, y: number): number {
  let res = 0;

  while (x > 0 && y > 0) {
    const curX = x & 1;
    const curY = y & 1;
    if (curX !== curY) {
      res++;
    }
    x = x >> 1;
    y = y >> 1;
  }

  while (x > 0) {
    if (x & 1) {
      res++;
    }
    x = x >> 1;
  }

  while (y > 0) {
    if (y & 1) {
      res++;
    }
    y = y >> 1;
  }

  return res;
};

```
## My Notes - 我的笔记


No notes

