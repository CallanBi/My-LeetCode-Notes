
# 剑指 Offer 63. 股票的最大利润  LCOF - 股票的最大利润

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Array-数组-blue.svg">   <img src="https://img.shields.io/badge/Dynamic Programming-动态规划-blue.svg">  


## Description - 题目描述

### EN:
English description is not available for the problem. Please switch to Chinese.

### ZH-CN:
<p>假设把某股票的价格按照时间先后顺序存储在数组中，请问买卖该股票一次可能获得的最大利润是多少？</p>

<p>&nbsp;</p>

<p><strong>示例 1:</strong></p>

<pre><strong>输入:</strong> [7,1,5,3,6,4]
<strong>输出:</strong> 5
<strong>解释: </strong>在第 2 天（股票价格 = 1）的时候买入，在第 5 天（股票价格 = 6）的时候卖出，最大利润 = 6-1 = 5 。
     注意利润不能是 7-1 = 6, 因为卖出价格需要大于买入价格。
</pre>

<p><strong>示例 2:</strong></p>

<pre><strong>输入:</strong> [7,6,4,3,1]
<strong>输出:</strong> 0
<strong>解释: </strong>在这种情况下, 没有交易完成, 所以最大利润为 0。</pre>

<p>&nbsp;</p>

<p><strong>限制：</strong></p>

<p><code>0 &lt;= 数组长度 &lt;= 10^5</code></p>

<p>&nbsp;</p>

<p><strong>注意：</strong>本题与主站 121 题相同：<a href="https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock/">https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock/</a></p>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/gu-piao-de-zui-da-li-run-lcof/description/)  -  [LeetCode-CN](https://leetcode-cn.com/problems/gu-piao-de-zui-da-li-run-lcof/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| typescript  | 64 ms | 42.7 MB | 2022/04/30 12:45 |

```typescript

function maxProfit(prices: number[]): number {
  if (prices.length === 0 || prices.length === 1) {
    return 0;
  }
  let res = 0, min = prices[0];
  for (let i = 1; i < prices.length; i++) {
    if (prices[i] < min) {
      min = prices[i];
    } else {
      const val = prices[i] - min;
      if (val > res) {
        res = val;
      }
    }
  }

  return res;
};

```
## My Notes - 我的笔记


思路：记住前面 i - 1 个数字的最小值。

```typescript
function maxProfit(prices: number[]): number {
  if (prices.length === 0 || prices.length === 1) {
    return 0;
  }
  let res = 0, min = prices[0];
  for (let i = 1; i < prices.length; i++) {
    if (prices[i] < min) {
      min = prices[i];
    } else {
      const val = prices[i] - min;
      if (val > res) {
        res = val;
      }
    }
  }

  return res;
};
```

