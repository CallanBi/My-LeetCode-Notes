
# 剑指 Offer 56 - I. 数组中数字出现的次数 LCOF - 数组中数字出现的次数

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Bit Manipulation-位运算-blue.svg">   <img src="https://img.shields.io/badge/Array-数组-blue.svg">  


## Description - 题目描述

### EN:
<p>English description is not available for the problem. Please switch to Chinese.</p>


### ZH-CN:
<p>一个整型数组 <code>nums</code> 里除两个数字之外，其他数字都出现了两次。请写程序找出这两个只出现一次的数字。要求时间复杂度是O(n)，空间复杂度是O(1)。</p>

<p>&nbsp;</p>

<p><strong>示例 1：</strong></p>

<pre><strong>输入：</strong>nums = [4,1,4,6]
<strong>输出：</strong>[1,6] 或 [6,1]
</pre>

<p><strong>示例 2：</strong></p>

<pre><strong>输入：</strong>nums = [1,2,10,4,1,4,3,3]
<strong>输出：</strong>[2,10] 或 [10,2]</pre>

<p>&nbsp;</p>

<p><strong>限制：</strong></p>

<ul>
	<li><code>2 &lt;= nums.length &lt;= 10000</code></li>
</ul>

<p>&nbsp;</p>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/shu-zu-zhong-shu-zi-chu-xian-de-ci-shu-lcof/description/)  -  [LeetCode-CN](https://leetcode-cn.com/problems/shu-zu-zhong-shu-zi-chu-xian-de-ci-shu-lcof/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| typescript  | 84 ms | 47.4 MB | 2022/04/17 19:21 |

```typescript

function singleNumbers(nums: number[]): number[] {
  if (nums.length === 2) {
    return nums;
  }

  const xorAll: (nums: number[]) => number = (nums) => nums.reduce((acc, cur) => {
    return acc ^ cur;
  }, 0);

  const pre = xorAll(nums);

  const preStr = pre.toString(2);

  const len = preStr.length;

  const idx = preStr.split('').lastIndexOf('1');

  const distance = len - idx;

  const group1: number[] = [];

  const group2: number[] = [];

  nums.forEach(i => {
    const origin = i.toString(2);
    const originLen = origin.length;

    if (origin[originLen - distance] === '1') {
      group1.push(i);
    } else {
      group2.push(i);
    }
  });

  const res1 = xorAll(group1);
  const res2 = xorAll(group2);

  return [res1, res2];
};

```
## My Notes - 我的笔记


按照剑指 offer 的思路，也是官方题解的思路来写。

遍历一遍数组对所有元素进行异或运算，将得到的结果的二进制中，找到第一个（或是随便一个）为 1 的位。

再遍历一遍数组，以这一位是否为1进行分组。由于异或的运算逻辑是不同则为1（可以理解为不进位加法），这两个数字一定被分到不同的组。

分组后，再对这两个数组的所有元素进行异或运算，最后的结果就是只出现一次的数字。

JavaScript 中 异或运算符为 `^`。（注意别和幂运算 `**` 搞混了）

```typescript
function singleNumbers(nums: number[]): number[] {
  if (nums.length === 2) {
    return nums;
  }

  const xorAll: (nums: number[]) => number = (nums) => nums.reduce((acc, cur) => {
    return acc ^ cur;
  }, 0);

  const pre = xorAll(nums);

  const preStr = pre.toString(2);

  const len = preStr.length;

  const idx = preStr.split('').lastIndexOf('1');

  const distance = len - idx;

  const group1: number[] = [];

  const group2: number[] = [];

  nums.forEach(i => {
    const origin = i.toString(2);
    const originLen = origin.length;

    if (origin[originLen - distance] === '1') {
      group1.push(i);
    } else {
      group2.push(i);
    }
  });

  const res1 = xorAll(group1);
  const res2 = xorAll(group2);

  return [res1, res2];
};
```

**注意点：**

数字调用\`toString(2)\` 方法后转化为二进制数，这时候最后的结果中字符串的长度可能不一。

在我最初的实现中，在第二次第二次遍历时，如果遍历数组时该元素转二进制字符串的长度大于最初对所有元素异或转二进制字符串的长度，则裁剪；如果不够，则高位补零：

```typescript
  const len = preStr.length;

  const idx = preStr.split('').lastIndexOf('1');

  const group1: number[] = [];

  const group2: number[] = [];

  nums.forEach(i => {
    const origin = i.toString(2);
    const originLen = origin.length;
    let formatted = '';
    if (originLen >= len) {
      formatted = origin.slice(origin.length - len);
    } else {
      let prefix = '';
      for (let i = 0; i < len - originLen; i++) {
        prefix += '0';
      }
      formatted = `${prefix}${origin}`;
    }
    if (formatted[idx] !== '1') {
      group1.push(i);
    } else {
      group2.push(i);
    }
  });
```
但裁剪和补零的时间复杂度都是$O(n)$，这样就不符合题目要求了。实际上这里是不需要要求这两个字符串长度相等的。只需要得第一次遍历的结果中，1出现的位置距离最后一位的距离 `distance`，就可以根据这个相对位置来判断了。

