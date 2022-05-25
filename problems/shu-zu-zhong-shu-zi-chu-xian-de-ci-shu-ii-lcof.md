
# 剑指 Offer 56 - II. 数组中数字出现的次数 II LCOF - 数组中数字出现的次数 II

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Bit Manipulation-位运算-blue.svg">   <img src="https://img.shields.io/badge/Array-数组-blue.svg">  


## Description - 题目描述

### EN:
<p>English description is not available for the problem. Please switch to Chinese.</p>


### ZH-CN:
<p>在一个数组 <code>nums</code> 中除一个数字只出现一次之外，其他数字都出现了三次。请找出那个只出现一次的数字。</p>

<p>&nbsp;</p>

<p><strong>示例 1：</strong></p>

<pre><strong>输入：</strong>nums = [3,4,3,3]
<strong>输出：</strong>4
</pre>

<p><strong>示例 2：</strong></p>

<pre><strong>输入：</strong>nums = [9,1,7,9,7,9,7]
<strong>输出：</strong>1</pre>

<p>&nbsp;</p>

<p><strong>限制：</strong></p>

<ul>
	<li><code>1 &lt;= nums.length &lt;= 10000</code></li>
	<li><code>1 &lt;= nums[i] &lt; 2^31</code></li>
</ul>

<p>&nbsp;</p>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/shu-zu-zhong-shu-zi-chu-xian-de-ci-shu-ii-lcof/description/)  -  [LeetCode-CN](https://leetcode.cn/problems/shu-zu-zhong-shu-zi-chu-xian-de-ci-shu-ii-lcof/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| typescript  | 204 ms | 66.5 MB | 2022/04/22 22:20 |

```typescript

function singleNumber(nums: number[]): number {
  if (nums.length === 1) {
    return nums[0];
  }
  const binaryArr = nums.map(i => i.toString(2)?.split(''))?.map(i => {
    const len = i?.length || 0;

    if (len < 31) {
      return [...new Array(31 - len).fill('0'), ...i];
    }
    return i;
  }) as string[][];

  const digitTotals = new Array(31).fill(0);

  binaryArr.forEach(i => {
    for (let j = 0; j < 31; j++) {
      digitTotals[j] += parseInt(i[j]);
    }
  });

  const ans = parseInt((digitTotals.map(i => i % 3).join('') as string), 2);

  return ans;

};

```
## My Notes - 我的笔记


用剑指 offer 的思路写的，不过我习惯写函数式编程风格的代码了，这样写的话时间复杂度反而更高。

剑指 offer 的思路就是，遍历一遍数字同时，找到其二进制表达，对每一位都加起来。最后的结果中某一位被3 整除的话，那唯一出现的数字中该位就为 0，否则为1。

然后在转为10进制就好了。

```typescript
function singleNumber(nums: number[]): number {
  if (nums.length === 1) {
    return nums[0];
  }
  const binaryArr = nums.map(i => i.toString(2)?.split(''))?.map(i => {
    const len = i?.length || 0;

    if (len < 31) {
      return [...new Array(31 - len).fill('0'), ...i];
    }
    return i;
  }) as string[][];

  const digitTotals = new Array(31).fill(0);

  binaryArr.forEach(i => {
    for (let j = 0; j < 31; j++) {
      digitTotals[j] += parseInt(i[j]);
    }
  });

  const ans = parseInt((digitTotals.map(i => i % 3).join('') as string), 2);

  return ans;

};
```

用面相过程的思想写代码的话时间复杂度肯定能更优一些，搞到 $O(n)$。

如果用哈希表解决的话，空间复杂度需要$O(n)$。但如果是剑指 offer 的思路，然后面相过程地去解决的话，只需要长度为 31 的数组即可，即空间复杂度为常数。


