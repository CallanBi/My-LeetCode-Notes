
# 剑指 Offer 61. 扑克牌中的顺子  LCOF - 扑克牌中的顺子

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Array-数组-blue.svg">   <img src="https://img.shields.io/badge/Sorting-排序-blue.svg">  


## Description - 题目描述

### EN:
English description is not available for the problem. Please switch to Chinese.

### ZH-CN:
<p>从<strong>若干副扑克牌</strong>中随机抽 <code>5</code> 张牌，判断是不是一个顺子，即这5张牌是不是连续的。2～10为数字本身，A为1，J为11，Q为12，K为13，而大、小王为 0 ，可以看成任意数字。A 不能视为 14。</p>

<p>&nbsp;</p>

<p><strong>示例&nbsp;1:</strong></p>

<pre>
<strong>输入:</strong> [1,2,3,4,5]
<strong>输出:</strong> True</pre>

<p>&nbsp;</p>

<p><strong>示例&nbsp;2:</strong></p>

<pre>
<strong>输入:</strong> [0,0,1,2,5]
<strong>输出:</strong> True</pre>

<p>&nbsp;</p>

<p><strong>限制：</strong></p>

<p>数组长度为 5&nbsp;</p>

<p>数组的数取值为 [0, 13] .</p>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/bu-ke-pai-zhong-de-shun-zi-lcof/description/)  -  [LeetCode-CN](https://leetcode-cn.com/problems/bu-ke-pai-zhong-de-shun-zi-lcof/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| typescript  | 60 ms | 43.8 MB | 2022/04/26 21:03 |

```typescript


function isStraight(nums: number[]): boolean {
  const sorted = nums.sort((a, b) => a - b);

  let zeroLen = 0;

  for (let i = 0; i < sorted.length; i++) {
    if (sorted[i] === 0) {
      zeroLen++;
    } else {
      if (sorted[i - 1] === undefined || sorted[i - 1] === 0 || sorted[i-1] + 1 === sorted[i]) {
        continue;
      }

      if (sorted[i - 1] === sorted[i]) {
        return false;
      }

      if (sorted[i-1] + 1 !== sorted[i]) {
        const distance = Math.abs(sorted[i] - sorted[i-1]) - 1;
        if (distance > zeroLen || zeroLen === 0) {
          return false;
        } else {
          zeroLen -= distance;
        }
      }
    }
  }

  return true;
}

```
## My Notes - 我的笔记


用剑指 offer 的思路。

先排序；
统计 0 的个数；
统计相邻数字的空缺，与 0 的个数比较。

