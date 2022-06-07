
# 96. Unique Binary Search Trees - 不同的二叉搜索树

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Tree-树-blue.svg">   <img src="https://img.shields.io/badge/Binary Search Tree-二叉搜索树-blue.svg">   <img src="https://img.shields.io/badge/Math-数学-blue.svg">   <img src="https://img.shields.io/badge/Dynamic Programming-动态规划-blue.svg">   <img src="https://img.shields.io/badge/Binary Tree-二叉树-blue.svg">  


## Description - 题目描述

### EN:
<p>Given an integer <code>n</code>, return <em>the number of structurally unique <strong>BST&#39;</strong>s (binary search trees) which has exactly </em><code>n</code><em> nodes of unique values from</em> <code>1</code> <em>to</em> <code>n</code>.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2021/01/18/uniquebstn3.jpg" style="width: 600px; height: 148px;" />
<pre>
<strong>Input:</strong> n = 3
<strong>Output:</strong> 5
</pre>

<p><strong>Example 2:</strong></p>

<pre>
<strong>Input:</strong> n = 1
<strong>Output:</strong> 1
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= n &lt;= 19</code></li>
</ul>


### ZH-CN:
<p>给你一个整数 <code>n</code> ，求恰由 <code>n</code> 个节点组成且节点值从 <code>1</code> 到 <code>n</code> 互不相同的 <strong>二叉搜索树</strong> 有多少种？返回满足题意的二叉搜索树的种数。</p>

<p> </p>

<p><strong>示例 1：</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2021/01/18/uniquebstn3.jpg" style="width: 600px; height: 148px;" />
<pre>
<strong>输入：</strong>n = 3
<strong>输出：</strong>5
</pre>

<p><strong>示例 2：</strong></p>

<pre>
<strong>输入：</strong>n = 1
<strong>输出：</strong>1
</pre>

<p> </p>

<p><strong>提示：</strong></p>

<ul>
	<li><code>1 <= n <= 19</code></li>
</ul>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/unique-binary-search-trees/description/)  -  [LeetCode-CN](https://leetcode.cn/problems/unique-binary-search-trees/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| golang  | 0 ms | 1.8 MB | 2022/06/07 13:01 |

```golang

func numTrees(n int) int {
  if n == 1 {
    return 1
  }

  mem := make(map[int]int)

  var recursive func(num int) int
  recursive = func(num int) int {
    if num == 0 {
      return 1
    }
    if num == 1 {
      return 1
    }

    ele, ok := mem[num]

    if ok {
      return ele
    }

    ret := 0
    for i := 1; i <= num; i++ {
      ret += recursive(i - 1) * recursive(num - i) 
    }
    mem[num] = ret
    return ret
  }

  return recursive(n)
}

```
## My Notes - 我的笔记


[官方题解](https://leetcode.cn/problems/unique-binary-search-trees/solution/bu-tong-de-er-cha-sou-suo-shu-by-leetcode-solution/)中的 dp 方法和卡特兰数用到数学推导，还是比较难想的。

直接用递归+记忆化搜索即可：

```go
func numTrees(n int) int {
  if n == 1 {
    return 1
  }

  mem := make(map[int]int)

  var recursive func(num int) int
  recursive = func(num int) int {
    if num == 0 {
      return 1
    }
    if num == 1 {
      return 1
    }

    ele, ok := mem[num]

    if ok {
      return ele
    }

    ret := 0
    for i := 1; i <= num; i++ {
      ret += recursive(i - 1) * recursive(num - i) 
    }
    mem[num] = ret
    return ret
  }

  return recursive(n)
}
```

