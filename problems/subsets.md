
# 78. Subsets - 子集

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Bit Manipulation-位运算-blue.svg">   <img src="https://img.shields.io/badge/Array-数组-blue.svg">   <img src="https://img.shields.io/badge/Backtracking-回溯-blue.svg">  


## Description - 题目描述

### EN:
<p>Given an integer array <code>nums</code> of <strong>unique</strong> elements, return <em>all possible subsets (the power set)</em>.</p>

<p>The solution set <strong>must not</strong> contain duplicate subsets. Return the solution in <strong>any order</strong>.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>

<pre>
<strong>Input:</strong> nums = [1,2,3]
<strong>Output:</strong> [[],[1],[2],[1,2],[3],[1,3],[2,3],[1,2,3]]
</pre>

<p><strong>Example 2:</strong></p>

<pre>
<strong>Input:</strong> nums = [0]
<strong>Output:</strong> [[],[0]]
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= nums.length &lt;= 10</code></li>
	<li><code>-10 &lt;= nums[i] &lt;= 10</code></li>
	<li>All the numbers of&nbsp;<code>nums</code> are <strong>unique</strong>.</li>
</ul>


### ZH-CN:
<p>给你一个整数数组 <code>nums</code> ，数组中的元素 <strong>互不相同</strong> 。返回该数组所有可能的子集（幂集）。</p>

<p>解集 <strong>不能</strong> 包含重复的子集。你可以按 <strong>任意顺序</strong> 返回解集。</p>

<p> </p>

<p><strong>示例 1：</strong></p>

<pre>
<strong>输入：</strong>nums = [1,2,3]
<strong>输出：</strong>[[],[1],[2],[1,2],[3],[1,3],[2,3],[1,2,3]]
</pre>

<p><strong>示例 2：</strong></p>

<pre>
<strong>输入：</strong>nums = [0]
<strong>输出：</strong>[[],[0]]
</pre>

<p> </p>

<p><strong>提示：</strong></p>

<ul>
	<li><code>1 <= nums.length <= 10</code></li>
	<li><code>-10 <= nums[i] <= 10</code></li>
	<li><code>nums</code> 中的所有元素 <strong>互不相同</strong></li>
</ul>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/subsets/description/)  -  [LeetCode-CN](https://leetcode.cn/problems/subsets/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| typescript  | 56 ms | 44.3 MB | 2022/06/01 23:03 |

```typescript

function subsets(nums: number[]): number[][] {
  if (nums.length === 1) {
    return [[], nums];
  }

  const res = [];

  const backtrack = (path: number[], idx: number) => {
    if (idx === nums.length) {
      res.push([...path]);
      return;
    }
    path.push(nums[idx]);
    backtrack(path, idx + 1);
    path.pop();
    backtrack(path, idx + 1);
  }

  backtrack([], 0);

  return res;
};

```
## My Notes - 我的笔记


思路1：对每一个元素与之前的元素组合：

```typescript
function subsets(nums: number[]): number[][] {
  if (nums.length === 1) {
    return [[], nums];
  }

  const res = [[]];

  for (let i = 0; i < nums.length; i++) {
    const len = res.length;
    for (let j = 0; j < len; j++) {
      res.push([...res[j], nums[i]]);
    }
  }

  return res;
};
```

思路2：回溯

[C++ 总结了回溯问题类型 带你搞懂回溯算法(大量例题)](https://leetcode.cn/problems/subsets/solution/c-zong-jie-liao-hui-su-wen-ti-lei-xing-dai-ni-gao-/)

上面的链接参考思想即可，代码不要借鉴。

还是参考[官方题解](https://leetcode.cn/problems/subsets/solution/zi-ji-by-leetcode-solution/)的第二种方法写的代码：

```typescript
function subsets(nums: number[]): number[][] {
  if (nums.length === 1) {
    return [[], nums];
  }

  const res = [];

  const backtrack = (path: number[], idx: number) => {
    if (idx === nums.length) {
      res.push([...path]);
      return;
    }
    path.push(nums[idx]);
    backtrack(path, idx + 1);
    path.pop();
    backtrack(path, idx + 1);
  }

  backtrack([], 0);

  return res;
};
```

`push()` 了之后递归，又 `pop()`了之后再递归，即是考虑当前选项和不考虑当前选项的两种方案。这比把`path`重新复制一遍性能要好。

但最后找到答案后还是要复制一遍 `path` 推到 `res` 中。



