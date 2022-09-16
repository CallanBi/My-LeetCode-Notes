
# 39. Combination Sum - 组合总和

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Array-数组-blue.svg">   <img src="https://img.shields.io/badge/Backtracking-回溯-blue.svg">  


## Description - 题目描述

### EN:
<p>Given an array of <strong>distinct</strong> integers <code>candidates</code> and a target integer <code>target</code>, return <em>a list of all <strong>unique combinations</strong> of </em><code>candidates</code><em> where the chosen numbers sum to </em><code>target</code><em>.</em> You may return the combinations in <strong>any order</strong>.</p>

<p>The <strong>same</strong> number may be chosen from <code>candidates</code> an <strong>unlimited number of times</strong>. Two combinations are unique if the frequency of at least one of the chosen numbers is different.</p>

<p>The test cases are generated such that the number of unique combinations that sum up to <code>target</code> is less than <code>150</code> combinations for the given input.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>

<pre>
<strong>Input:</strong> candidates = [2,3,6,7], target = 7
<strong>Output:</strong> [[2,2,3],[7]]
<strong>Explanation:</strong>
2 and 3 are candidates, and 2 + 2 + 3 = 7. Note that 2 can be used multiple times.
7 is a candidate, and 7 = 7.
These are the only two combinations.
</pre>

<p><strong>Example 2:</strong></p>

<pre>
<strong>Input:</strong> candidates = [2,3,5], target = 8
<strong>Output:</strong> [[2,2,2,2],[2,3,3],[3,5]]
</pre>

<p><strong>Example 3:</strong></p>

<pre>
<strong>Input:</strong> candidates = [2], target = 1
<strong>Output:</strong> []
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= candidates.length &lt;= 30</code></li>
	<li><code>2 &lt;= candidates[i] &lt;= 40</code></li>
	<li>All elements of <code>candidates</code> are <strong>distinct</strong>.</li>
	<li><code>1 &lt;= target &lt;= 500</code></li>
</ul>


### ZH-CN:
<p>给你一个 <strong>无重复元素</strong> 的整数数组&nbsp;<code>candidates</code> 和一个目标整数&nbsp;<code>target</code>&nbsp;，找出&nbsp;<code>candidates</code>&nbsp;中可以使数字和为目标数&nbsp;<code>target</code> 的 <em>所有&nbsp;</em><strong>不同组合</strong> ，并以列表形式返回。你可以按 <strong>任意顺序</strong> 返回这些组合。</p>

<p><code>candidates</code> 中的 <strong>同一个</strong> 数字可以 <strong>无限制重复被选取</strong> 。如果至少一个数字的被选数量不同，则两种组合是不同的。&nbsp;</p>

<p>对于给定的输入，保证和为&nbsp;<code>target</code> 的不同组合数少于 <code>150</code> 个。</p>

<p>&nbsp;</p>

<p><strong>示例&nbsp;1：</strong></p>

<pre>
<strong>输入：</strong>candidates = <code>[2,3,6,7], </code>target = <code>7</code>
<strong>输出：</strong>[[2,2,3],[7]]
<strong>解释：</strong>
2 和 3 可以形成一组候选，2 + 2 + 3 = 7 。注意 2 可以使用多次。
7 也是一个候选， 7 = 7 。
仅有这两种组合。</pre>

<p><strong>示例&nbsp;2：</strong></p>

<pre>
<strong>输入: </strong>candidates = [2,3,5]<code>, </code>target = 8
<strong>输出: </strong>[[2,2,2,2],[2,3,3],[3,5]]</pre>

<p><strong>示例 3：</strong></p>

<pre>
<strong>输入: </strong>candidates = <code>[2], </code>target = 1
<strong>输出: </strong>[]
</pre>

<p>&nbsp;</p>

<p><strong>提示：</strong></p>

<ul>
	<li><code>1 &lt;= candidates.length &lt;= 30</code></li>
	<li><code>1 &lt;= candidates[i] &lt;= 200</code></li>
	<li><code>candidate</code> 中的每个元素都 <strong>互不相同</strong></li>
	<li><code>1 &lt;= target &lt;= 500</code></li>
</ul>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/combination-sum/description/)  -  [LeetCode-CN](https://leetcode.cn/problems/combination-sum/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| typescript  | 76 ms | 46.5 MB | 2022/05/08 22:18 |

```typescript

function combinationSum(candidates: number[], target: number): number[][] {
  const ans: number[][] = [];
  const dfs = (target: number, path: number[], idx: number) => {
    if (idx === candidates.length) {
      return;
    }
    if (target === 0) {
      ans.push(path);
      return;
    }
    // 直接跳过
    dfs(target, path, idx + 1);
    // 选择当前数
    if (target - candidates[idx] >= 0) {
      dfs(target - candidates[idx], [...path, candidates[idx]], idx);
    }
  }

  dfs(target, [], 0);
  return ans;
};

```
## My Notes - 我的笔记


最开始的朴素回溯思想:

```typescript
function combinationSum(candidates: number[], target: number): number[][] {
  const res: number[][] = [];

  const recur: (idx: number, sum: number, path: number[]) => void = (idx, sum, path) => {
    if (sum >= target || idx === candidates.length) {
      return;
    }

    let rest = target - sum;

    recur(idx + 1, sum, path);

    if (rest % candidates[idx] === 0) {
      const time = rest / candidates[idx];
      const item = [...path];
      let curSum = sum;
      for (let i = 0; i < time; i++) {
        curSum += candidates[idx];
        item.push(candidates[idx]);
        if (i !== time - 1) {
          recur(idx + 1, curSum, [...item]);
        } else {
          res.push(item);
          recur(idx + 1, 0, []);
        }
      }

    } else {
      const time = Math.floor(rest / candidates[idx]);
      const item = [...path];
      let curSum = sum;
      for (let i = 0; i < time; i++) {
        curSum += candidates[idx];
        item.push(candidates[idx]);
        recur(idx + 1, curSum, [...item]);
      }
    }
  }

  recur(0, 0, []);


  const isEqual: (arr1: number[], arr2: number[]) => boolean = (arr1, arr2) => {
    if (arr1.length !== arr2.length) {
      return false;
    }

    for (let i = 0; i < arr1.length; i++) {
      if (arr1[i] !== arr2[i]) {
        return false;
      }
    }
    return true;
  }

  for (let i = 0; i < res.length; i++) {
    for (let j = i + 1; j < res.length; j++) {
      if (isEqual(res[i], res[j])) {
        res.splice(j, 1);
        j--;
      }
    }
  }

  return res;

};
```

后来参考了[官方题解](https://leetcode-cn.com/problems/combination-sum/solution/zu-he-zong-he-by-leetcode-solution/)发现，对于选择当前数，不需要做额外的处理，只需要 dfs `target - 当前数`，然后 `path` 中推入当前数即可。

```typescript
function combinationSum(candidates: number[], target: number): number[][] {
  const ans: number[][] = [];
  const dfs = (target: number, path: number[], idx: number) => {
    if (idx === candidates.length) {
      return;
    }
    if (target === 0) {
      ans.push(path);
      return;
    }
    // 直接跳过
    dfs(target, path, idx + 1);
    // 选择当前数
    if (target - candidates[idx] >= 0) {
      dfs(target - candidates[idx], [...path, candidates[idx]], idx);
    }
  }

  dfs(target, [], 0);
  return ans;
};
```

> **时间复杂度**：$O(S)$，其中 $S$ 为所有可行解的长度之和。从分析给出的搜索树我们可以看出时间复杂度取决于搜索树所有叶子节点的深度之和，即所有可行解的长度之和。在这题中，我们很难给出一个比较紧的上界，我们知道 $O(n \times 2^n)$ 是一个比较松的上界，即在这份代码中，nn 个位置每次考虑选或者不选，如果符合条件，就加入答案的时间代价。但是实际运行的时候，因为不可能所有的解都满足条件，递归的时候我们还会用 $target−candidates[idx]≥0$ 进行剪枝，所以实际运行情况是远远小于这个上界的。&#x20;
>
> **空间复杂度**：$O(target)$。除答案数组外，空间复杂度取决于递归的栈深度，在最差情况下需要递归 $O(target)$ 层。


