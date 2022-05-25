
# 55. Jump Game - 跳跃游戏

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Greedy-贪心-blue.svg">   <img src="https://img.shields.io/badge/Array-数组-blue.svg">   <img src="https://img.shields.io/badge/Dynamic Programming-动态规划-blue.svg">  


## Description - 题目描述

### EN:
<p>You are given an integer array <code>nums</code>. You are initially positioned at the array&#39;s <strong>first index</strong>, and each element in the array represents your maximum jump length at that position.</p>

<p>Return <code>true</code><em> if you can reach the last index, or </em><code>false</code><em> otherwise</em>.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>

<pre>
<strong>Input:</strong> nums = [2,3,1,1,4]
<strong>Output:</strong> true
<strong>Explanation:</strong> Jump 1 step from index 0 to 1, then 3 steps to the last index.
</pre>

<p><strong>Example 2:</strong></p>

<pre>
<strong>Input:</strong> nums = [3,2,1,0,4]
<strong>Output:</strong> false
<strong>Explanation:</strong> You will always arrive at index 3 no matter what. Its maximum jump length is 0, which makes it impossible to reach the last index.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= nums.length &lt;= 10<sup>4</sup></code></li>
	<li><code>0 &lt;= nums[i] &lt;= 10<sup>5</sup></code></li>
</ul>


### ZH-CN:
<p>给定一个非负整数数组 <code>nums</code> ，你最初位于数组的 <strong>第一个下标</strong> 。</p>

<p>数组中的每个元素代表你在该位置可以跳跃的最大长度。</p>

<p>判断你是否能够到达最后一个下标。</p>

<p> </p>

<p><strong>示例 1：</strong></p>

<pre>
<strong>输入：</strong>nums = [2,3,1,1,4]
<strong>输出：</strong>true
<strong>解释：</strong>可以先跳 1 步，从下标 0 到达下标 1, 然后再从下标 1 跳 3 步到达最后一个下标。
</pre>

<p><strong>示例 2：</strong></p>

<pre>
<strong>输入：</strong>nums = [3,2,1,0,4]
<strong>输出：</strong>false
<strong>解释：</strong>无论怎样，总会到达下标为 3 的位置。但该下标的最大跳跃长度是 0 ， 所以永远不可能到达最后一个下标。
</pre>

<p> </p>

<p><strong>提示：</strong></p>

<ul>
	<li><code>1 <= nums.length <= 3 * 10<sup>4</sup></code></li>
	<li><code>0 <= nums[i] <= 10<sup>5</sup></code></li>
</ul>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/jump-game/description/)  -  [LeetCode-CN](https://leetcode-cn.com/problems/jump-game/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| python3  | 128 ms | 16.1 MB | 2022/05/25 22:14 |

```python3

class Solution:
    def canJump(self, nums: List[int]) -> bool:
      n, rightmost = len(nums), 0
      for i in range(n):
          if i <= rightmost:
              rightmost = max(rightmost, i + nums[i])
              if rightmost >= n - 1:
                  return True
      return False

```
## My Notes - 我的笔记


note test for leetecho



刚开始感觉还是典型的递归+记忆化搜索：

```typescript
function canJump(nums: number[]): boolean {
  function recur(idx: number): boolean {
    const mem: Map<number, boolean> = new Map();
    if (idx >= nums.length - 1) {
      return true;
    }
    const memEle = mem.get(idx);
    if (memEle !== undefined) {
      return memEle;
    }
    let res = false;
    for (let i = idx + 1; (i < idx + nums[idx] + 1) && (i < nums.length); i++) {
      res = res || recur(i);
    }
    mem.set(idx, res);
    return res;
  }

  if (nums.length === 1) {
    return true;
  }

  return recur(0);

};
```

但是会超出时间限制，算了一下时间复杂度应该是$O(n^2)$，不太行。

参考了答案之后的做法：

```python
class Solution:
    def canJump(self, nums: List[int]) -> bool:
      n, rightmost = len(nums), 0
      for i in range(n):
          if i <= rightmost:
              rightmost = max(rightmost, i + nums[i])
              if rightmost >= n - 1:
                  return True
      return False
```

最近在写 Python，所以用 Python 刷题也未尝不可✍️


