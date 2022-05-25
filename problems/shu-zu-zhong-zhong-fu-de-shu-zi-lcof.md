
# 剑指 Offer 03. 数组中重复的数字 LCOF - 数组中重复的数字

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Array-数组-blue.svg">   <img src="https://img.shields.io/badge/Hash Table-哈希表-blue.svg">   <img src="https://img.shields.io/badge/Sorting-排序-blue.svg">  


## Description - 题目描述

### EN:
<p>English description is not available for the problem. Please switch to Chinese.</p>


### ZH-CN:
<p>找出数组中重复的数字。</p>

<p><br>
在一个长度为 n 的数组 nums 里的所有数字都在 0～n-1 的范围内。数组中某些数字是重复的，但不知道有几个数字重复了，也不知道每个数字重复了几次。请找出数组中任意一个重复的数字。</p>

<p><strong>示例 1：</strong></p>

<pre><strong>输入：</strong>
[2, 3, 1, 0, 2, 5, 3]
<strong>输出：</strong>2 或 3 
</pre>

<p>&nbsp;</p>

<p><strong>限制：</strong></p>

<p><code>2 &lt;= n &lt;= 100000</code></p>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/shu-zu-zhong-zhong-fu-de-shu-zi-lcof/description/)  -  [LeetCode-CN](https://leetcode.cn/problems/shu-zu-zhong-zhong-fu-de-shu-zi-lcof/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| typescript  | 84 ms | 43.8 MB | 2021/04/03 20:31 |

```typescript

function findRepeatNumber(nums: number[]): number {
  // const s = new Set<number>();
  // for (const e of nums) {
  //  if(s.has(e)) {
  //     return e;
  //   } else {
  //     s.add(e);
  //   }
  // }
  for (let i = 0; i < nums.length; i++) {
    if (nums[i] !== i) {
      if (nums[i] === nums[nums[i]]) {
        return nums[i];
      } else {
        // 交换
        const temp = nums[i];
        nums[i] = nums[temp];
        nums[temp] = temp;
      }
    }
  }
};

```
## My Notes - 我的笔记


刚开始的解法

```typescript
function findRepeatNumber(nums: number[]): number {
  const numMap = {};
  nums.forEach(e => {
    if (!(e in numMap)) {
      numMap[e] = 1;
    } else {
      numMap[e] = numMap[e] + 1;
    }
  })
  const mostAppearNum = Math.max(...Object.values(numMap) as number[]);
  return Number(Object.entries(numMap).find(([k, v]) => 
    v === mostAppearNum
  )[0]) as number || null;
};
```
后来发现理解错题意了，不是找重复最多的数字，那直接用 set就行：
```typscript
const s = new Set<number>();
  for (const e of nums) {
   if(s.has(e)) {
      return e;
    } else {
      s.add(e);
    }
  }
```

用剑指 offer 的思路：
```typescript
for (let i = 0; i < nums.length; i++) {
    if (nums[i] !== i) {
      if (nums[i] === nums[nums[i]]) {
        return nums[i];
      } else {
        // 交换
        const temp = nums[i];
        nums[i] = nums[temp];
        nums[temp] = temp;
      }
    }
  }
```

