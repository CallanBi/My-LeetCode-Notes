
# 104. Maximum Depth of Binary Tree - 二叉树的最大深度

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Tree-树-blue.svg">   <img src="https://img.shields.io/badge/Depth First Search-深度优先搜索-blue.svg">   <img src="https://img.shields.io/badge/Breadth First Search-广度优先搜索-blue.svg">   <img src="https://img.shields.io/badge/Binary Tree-二叉树-blue.svg">  


## Description - 题目描述

### EN:
<p>Given the <code>root</code> of a binary tree, return <em>its maximum depth</em>.</p>

<p>A binary tree&#39;s <strong>maximum depth</strong>&nbsp;is the number of nodes along the longest path from the root node down to the farthest leaf node.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2020/11/26/tmp-tree.jpg" style="width: 400px; height: 277px;" />
<pre>
<strong>Input:</strong> root = [3,9,20,null,null,15,7]
<strong>Output:</strong> 3
</pre>

<p><strong>Example 2:</strong></p>

<pre>
<strong>Input:</strong> root = [1,null,2]
<strong>Output:</strong> 2
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li>The number of nodes in the tree is in the range <code>[0, 10<sup>4</sup>]</code>.</li>
	<li><code>-100 &lt;= Node.val &lt;= 100</code></li>
</ul>


### ZH-CN:
<p>给定一个二叉树，找出其最大深度。</p>

<p>二叉树的深度为根节点到最远叶子节点的最长路径上的节点数。</p>

<p><strong>说明:</strong>&nbsp;叶子节点是指没有子节点的节点。</p>

<p><strong>示例：</strong><br>
给定二叉树 <code>[3,9,20,null,null,15,7]</code>，</p>

<pre>    3
   / \
  9  20
    /  \
   15   7</pre>

<p>返回它的最大深度&nbsp;3 。</p>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/maximum-depth-of-binary-tree/description/)  -  [LeetCode-CN](https://leetcode.cn/problems/maximum-depth-of-binary-tree/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| golang  | 4 ms | 4.1 MB | 2022/06/10 15:35 |

```golang

/**
 * Definition for a binary tree node.
 * type TreeNode struct {
 *     Val int
 *     Left *TreeNode
 *     Right *TreeNode
 * }
 */
func maxDepth(root *TreeNode) int {
  if root == nil {
    return 0
  }
  // var depth int = 0
  var findDepth func(node *TreeNode, dep int) int

  findDepth = func(node *TreeNode, dep int) int {
    if node == nil {
      return dep
    }

    if node.Left == nil {
      if node.Right != nil {
        return findDepth(node.Right, dep+1)
      } else {
        return dep
      }
    }

    if node.Right == nil {
      if node.Left != nil {
        return findDepth(node.Left, dep+1)
      } else {
        return dep
      }
    }

    leftDepth := findDepth(node.Left, dep + 1)
    rightDepth := findDepth(node.Right, dep + 1)

    if leftDepth > rightDepth {
      return leftDepth
    } else {
      return rightDepth
    }
  }

  return findDepth(root, 1)
}

```
## My Notes - 我的笔记


递归即可。

```go
/**
 * Definition for a binary tree node.
 * type TreeNode struct {
 *     Val int
 *     Left *TreeNode
 *     Right *TreeNode
 * }
 */
func maxDepth(root *TreeNode) int {
  if root == nil {
    return 0
  }
  // var depth int = 0
  var findDepth func(node *TreeNode, dep int) int

  findDepth = func(node *TreeNode, dep int) int {
    if node == nil {
      return dep
    }

    if node.Left == nil {
      if node.Right != nil {
        return findDepth(node.Right, dep+1)
      } else {
        return dep
      }
    }

    if node.Right == nil {
      if node.Left != nil {
        return findDepth(node.Left, dep+1)
      } else {
        return dep
      }
    }

    leftDepth := findDepth(node.Left, dep + 1)
    rightDepth := findDepth(node.Right, dep + 1)

    if leftDepth > rightDepth {
      return leftDepth
    } else {
      return rightDepth
    }
  }

  return findDepth(root, 1)
}
```


