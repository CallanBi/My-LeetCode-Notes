
# 309. Best Time to Buy and Sell Stock with Cooldown - 买卖股票的最佳时机含冷冻期

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Array-数组-blue.svg">   <img src="https://img.shields.io/badge/Dynamic Programming-动态规划-blue.svg">  


## Description - 题目描述

### EN:
<p>You are given an array <code>prices</code> where <code>prices[i]</code> is the price of a given stock on the <code>i<sup>th</sup></code> day.</p>

<p>Find the maximum profit you can achieve. You may complete as many transactions as you like (i.e., buy one and sell one share of the stock multiple times) with the following restrictions:</p>

<ul>
	<li>After you sell your stock, you cannot buy stock on the next day (i.e., cooldown one day).</li>
</ul>

<p><strong>Note:</strong> You may not engage in multiple transactions simultaneously (i.e., you must sell the stock before you buy again).</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input:</strong> prices = [1,2,3,0,2]
<strong>Output:</strong> 3
<strong>Explanation:</strong> transactions = [buy, sell, cooldown, buy, sell]
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre>
<strong>Input:</strong> prices = [1]
<strong>Output:</strong> 0
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= prices.length &lt;= 5000</code></li>
	<li><code>0 &lt;= prices[i] &lt;= 1000</code></li>
</ul>


### ZH-CN:
<p>给定一个整数数组<meta charset="UTF-8" /><code>prices</code>，其中第&nbsp;<em>&nbsp;</em><code>prices[i]</code>&nbsp;表示第&nbsp;<code><em>i</em></code>&nbsp;天的股票价格 。​</p>

<p>设计一个算法计算出最大利润。在满足以下约束条件下，你可以尽可能地完成更多的交易（多次买卖一支股票）:</p>

<ul>
	<li>卖出股票后，你无法在第二天买入股票 (即冷冻期为 1 天)。</li>
</ul>

<p><strong>注意：</strong>你不能同时参与多笔交易（你必须在再次购买前出售掉之前的股票）。</p>

<p>&nbsp;</p>

<p><strong>示例 1:</strong></p>

<pre>
<strong>输入:</strong> prices = [1,2,3,0,2]
<strong>输出: </strong>3 
<strong>解释:</strong> 对应的交易状态为: [买入, 卖出, 冷冻期, 买入, 卖出]</pre>

<p><strong>示例 2:</strong></p>

<pre>
<strong>输入:</strong> prices = [1]
<strong>输出:</strong> 0
</pre>

<p>&nbsp;</p>

<p><strong>提示：</strong></p>

<ul>
	<li><code>1 &lt;= prices.length &lt;= 5000</code></li>
	<li><code>0 &lt;= prices[i] &lt;= 1000</code></li>
</ul>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-with-cooldown/description/)  -  [LeetCode-CN](https://leetcode.cn/problems/best-time-to-buy-and-sell-stock-with-cooldown/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| typescript  | 80 ms | 44 MB | 2023/03/29 19:53 |

```typescript

function maxProfit(prices: number[]): number {
  if (prices.length === 1) {
    return 0;
  }
  if (prices.length === 2) {
    return Math.max(prices[1] - prices[0], 0);
  }

  const cur = [0, 0], yesterday = [0, -prices[0]], beforeYesterday = [0, -Infinity];

  for (let i = 1; i < prices.length; i++) {
    cur[0] = Math.max(yesterday[1] + prices[i], yesterday[0]);
    cur[1] = Math.max(beforeYesterday[0] - prices[i], yesterday[1]);
    beforeYesterday[0] = yesterday[0];
    beforeYesterday[1] = yesterday[1];
    yesterday[0] = cur[0];
    yesterday[1] = cur[1];
  }

  return cur[0];
};

```
## My Notes - 我的笔记


参考了[股票问题系列通解](https://leetcode.cn/circle/article/qiAgHn/) 写出来的代码。
# 未优化空间
```typescript
function maxProfit(prices: number[]): number {
  if (prices.length === 1) {
    return 0;
  }
  if (prices.length === 2) {
    return Math.max(prices[1] - prices[0], 0);
  }

  const dp: number[][] = new Array(prices.length + 1).fill([]).map(i => new Array(2).fill(0));

  dp[0][1] = -Infinity;
  dp[1][1] = -prices[0];
  dp[2][1] = Math.max(-prices[1], -prices[0]);

  for (let i = 1; i < prices.length; i++) {
    dp[i + 1][0] = Math.max(dp[i][1] + prices[i], dp[i][0]);
    dp[i + 1][1] = Math.max(dp[i - 1][0] - prices[i], dp[i][1]);
  }

  return dp[prices.length][0];
};
```
注意：遍历`price[i]` 时，实际上是计算`dp[i+1]` 的状态，但 `price[i]` 不要一不小心写成`price[i+1]`了。


# 优化空间
`dp[i+1] `的状态只和 `dp[i-]` 和 `dp[i-1]` 有关，可以优化空间复杂度。

```typescript
function maxProfit(prices: number[]): number {
  if (prices.length === 1) {
    return 0;
  }
  if (prices.length === 2) {
    return Math.max(prices[1] - prices[0], 0);
  }

  const cur = [0, 0], yesterday = [0, -prices[0]], beforeYesterday = [0, -Infinity];

  for (let i = 1; i < prices.length; i++) {
    cur[0] = Math.max(yesterday[1] + prices[i], yesterday[0]);
    cur[1] = Math.max(beforeYesterday[0] - prices[i], yesterday[1]);
    beforeYesterday[0] = yesterday[0];
    beforeYesterday[1] = yesterday[1];
    yesterday[0] = cur[0];
    yesterday[1] = cur[1];
  }

  return cur[0];
};
```


