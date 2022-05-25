
# 剑指 Offer 43. 1～n整数中1出现的次数  LCOF - 1～n 整数中 1 出现的次数

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Recursion-递归-blue.svg">   <img src="https://img.shields.io/badge/Math-数学-blue.svg">   <img src="https://img.shields.io/badge/Dynamic Programming-动态规划-blue.svg">  


## Description - 题目描述

### EN:
English description is not available for the problem. Please switch to Chinese.

### ZH-CN:
<p>输入一个整数 <code>n</code> ，求1～n这n个整数的十进制表示中1出现的次数。</p>

<p>例如，输入12，1～12这些整数中包含1 的数字有1、10、11和12，1一共出现了5次。</p>

<p> </p>

<p><strong>示例 1：</strong></p>

<pre>
<strong>输入：</strong>n = 12
<strong>输出：</strong>5
</pre>

<p><strong>示例 2：</strong></p>

<pre>
<strong>输入：</strong>n = 13
<strong>输出：</strong>6</pre>

<p> </p>

<p><strong>限制：</strong></p>

<ul>
	<li><code>1 <= n < 2^31</code></li>
</ul>

<p>注意：本题与主站 233 题相同：<a href="https://leetcode-cn.com/problems/number-of-digit-one/">https://leetcode-cn.com/problems/number-of-digit-one/</a></p>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/1nzheng-shu-zhong-1chu-xian-de-ci-shu-lcof/description/)  -  [LeetCode-CN](https://leetcode-cn.com/problems/1nzheng-shu-zhong-1chu-xian-de-ci-shu-lcof/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| typescript  | 64 ms | 39.3 MB | 2021/12/16 16:25 |

```typescript

function countDigitOne(n: number): number {
  let place = 1, counter = 0, digit = n, high = 0, low = 0, cur = 0;
  while (digit !== 0) {
    cur = digit % 10;
    high = Math.floor(digit / 10);
    low = n % place;
    if (cur === 0) {
      counter += high * place;
    } else if (cur === 1) {
      counter += high * place + (low + 1);
    } else {
      counter += high * place + place;
    }
    digit = Math.floor(digit / 10);
    place *= 10;
  }
  return counter;
};

```
## My Notes - 我的笔记


本题与主站 233 题相同：https://leetcode-cn.com/problems/number-of-digit-one/

# 超出时间限制的最简单答案

```typescript
function countDigitOne(n: number): number {
  let counter = 0;
  for (let i = 1; i <= n; i++) {
    let cur = i;
    while (cur !== 0) {
      if (cur % 10 === 1) {
        counter++;
      }
      cur = Math.floor(cur / 10);
    }
  }
  return counter;
};
```

# 用数学规律找答案

参考了[这个题解](https://leetcode-cn.com/problems/1nzheng-shu-zhong-1chu-xian-de-ci-shu-lcof/solution/dong-hua-mo-ni-wo-tai-xi-huan-zhe-ge-ti-vxzwc/)之后：

```typescript
function countDigitOne(n: number): number {
  // place 代表位因子，个位的位因子为1, 十位 -> 100, 百位 -> 1000...
  let place = 1, counter = 0, digit = n, high = 0, low = 0, cur = 0;
  while (digit !== 0) {
    cur = digit % 10;
    high = Math.floor(digit / 10);
    low = n % place;
    if (cur === 0) {
      counter += high * place;
    } else if (cur === 1) {
      counter += high * place + (low + 1);
    } else {
      counter += high * place + place;
    }
    digit = Math.floor(digit / 10);
    place *= 10;
  }
  return counter;
};
```

# 用 数位 dp 的方法解决:

[什么是数位 dp](https://oi-wiki.org/dp/number/)

[题解参考](https://leetcode-cn.com/problems/number-of-digit-one/solution/shu-wei-dpjava-by-liweiwei1419-awxv/)

`dp1[i]` 是$  0 \sim 10^i - 1 $ 中 1 的个数。

`dp2[i]` 是 0 ~ 从右往左第 `i` 位所截取的数字 中 1 的个数。

代码：

```typescript
function countDigitOne(n: number): number {
  const numArr = n.toString().split('').reverse();
  const dp1: number[] = [];
  const dp2: number[] = [];

  dp1[0] = 1;

  dp2[0] = numArr[0] === '0' ? 0 : 1;

  for (let i = 1; i < numArr.length; i++) {
    dp1[i] = 10 * dp1[i-1] + Math.pow(10, i);

    if (numArr[i] === '0') {
      dp2[i] = dp2[i-1];
    } else if (numArr[i] === '1') {
      const rest = Number(numArr.slice(0, i).reverse().join('')) + 1;
      dp2[i] = dp1[i-1] + rest + dp2[i-1];
    } else {
      dp2[i] = (Number(numArr[i])) * dp1[i-1] + Math.pow(10, i) + dp2[i-1];
    }
  }

  return dp2[numArr.length-1];
};
```


