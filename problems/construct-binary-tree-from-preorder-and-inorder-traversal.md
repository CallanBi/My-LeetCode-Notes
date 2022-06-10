
# 105. Construct Binary Tree from Preorder and Inorder Traversal - 从前序与中序遍历序列构造二叉树

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Tree-树-blue.svg">   <img src="https://img.shields.io/badge/Array-数组-blue.svg">   <img src="https://img.shields.io/badge/Hash Table-哈希表-blue.svg">   <img src="https://img.shields.io/badge/Divide and Conquer-分治-blue.svg">   <img src="https://img.shields.io/badge/Binary Tree-二叉树-blue.svg">  


## Description - 题目描述

### EN:
<p>Given two integer arrays <code>preorder</code> and <code>inorder</code> where <code>preorder</code> is the preorder traversal of a binary tree and <code>inorder</code> is the inorder traversal of the same tree, construct and return <em>the binary tree</em>.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2021/02/19/tree.jpg" style="width: 277px; height: 302px;" />
<pre>
<strong>Input:</strong> preorder = [3,9,20,15,7], inorder = [9,3,15,20,7]
<strong>Output:</strong> [3,9,20,null,null,15,7]
</pre>

<p><strong>Example 2:</strong></p>

<pre>
<strong>Input:</strong> preorder = [-1], inorder = [-1]
<strong>Output:</strong> [-1]
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= preorder.length &lt;= 3000</code></li>
	<li><code>inorder.length == preorder.length</code></li>
	<li><code>-3000 &lt;= preorder[i], inorder[i] &lt;= 3000</code></li>
	<li><code>preorder</code> and <code>inorder</code> consist of <strong>unique</strong> values.</li>
	<li>Each value of <code>inorder</code> also appears in <code>preorder</code>.</li>
	<li><code>preorder</code> is <strong>guaranteed</strong> to be the preorder traversal of the tree.</li>
	<li><code>inorder</code> is <strong>guaranteed</strong> to be the inorder traversal of the tree.</li>
</ul>


### ZH-CN:
<p>给定两个整数数组&nbsp;<code>preorder</code> 和 <code>inorder</code>&nbsp;，其中&nbsp;<code>preorder</code> 是二叉树的<strong>先序遍历</strong>， <code>inorder</code>&nbsp;是同一棵树的<strong>中序遍历</strong>，请构造二叉树并返回其根节点。</p>

<p>&nbsp;</p>

<p><strong>示例 1:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2021/02/19/tree.jpg" style="height: 302px; width: 277px;" />
<pre>
<strong>输入</strong><strong>:</strong> preorder = [3,9,20,15,7], inorder = [9,3,15,20,7]
<strong>输出:</strong> [3,9,20,null,null,15,7]
</pre>

<p><strong>示例 2:</strong></p>

<pre>
<strong>输入:</strong> preorder = [-1], inorder = [-1]
<strong>输出:</strong> [-1]
</pre>

<p>&nbsp;</p>

<p><strong>提示:</strong></p>

<ul>
	<li><code>1 &lt;= preorder.length &lt;= 3000</code></li>
	<li><code>inorder.length == preorder.length</code></li>
	<li><code>-3000 &lt;= preorder[i], inorder[i] &lt;= 3000</code></li>
	<li><code>preorder</code>&nbsp;和&nbsp;<code>inorder</code>&nbsp;均 <strong>无重复</strong> 元素</li>
	<li><code>inorder</code>&nbsp;均出现在&nbsp;<code>preorder</code></li>
	<li><code>preorder</code>&nbsp;<strong>保证</strong> 为二叉树的前序遍历序列</li>
	<li><code>inorder</code>&nbsp;<strong>保证</strong> 为二叉树的中序遍历序列</li>
</ul>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/description/)  -  [LeetCode-CN](https://leetcode.cn/problems/construct-binary-tree-from-preorder-and-inorder-traversal/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| golang  | 4 ms | 4.1 MB | 2022/06/10 17:09 |

```golang

/**
 * Definition for a binary tree node.
 * type TreeNode struct {
 *     Val int
 *     Left *TreeNode
 *     Right *TreeNode
 * }
 */
func buildTree(preorder []int, inorder []int) *TreeNode {
  var buildTree func(preOrderStart int, preOrderEnd int, inOrderStart int, inOrderEnd int) *TreeNode
  buildTree = func(preOrderStart int, preOrderEnd int, inOrderStart int, inOrderEnd int) *TreeNode {
    if (preOrderStart >= len(preorder) || inOrderStart >= len(inorder) || preOrderEnd - preOrderStart == 0 || inOrderEnd - inOrderStart == 0) {
      return nil
    }

    if (preOrderEnd - preOrderStart == 1 || inOrderEnd - inOrderStart == 1) {
      return &TreeNode{ Val: preorder[preOrderStart], Left: nil, Right: nil }
    }

    inOrderNodeIdx := findIndex(inorder, preorder[preOrderStart], inOrderStart, inOrderEnd)

    leftLen := inOrderNodeIdx - inOrderStart

    leftTree := buildTree(preOrderStart+1, preOrderStart + 1 + leftLen, inOrderStart, inOrderNodeIdx)

    rightTree := buildTree(preOrderStart + 1 + leftLen, preOrderEnd, inOrderNodeIdx + 1, inOrderEnd)

    return &TreeNode{
      Val: preorder[preOrderStart],
      Left: leftTree,
      Right: rightTree,
    }
  }

  return buildTree(0, len(preorder), 0, len(inorder))
}

func findIndex(s []int, e int, start int, end int) int {
  for i := start; i < end; i++ {
    if (s[i] == e) {
      return i
    }
  }
  return -1
}

```
## My Notes - 我的笔记


以下中文由 Rime 输入法使用粤拼方案输入（初步尝试粤拼输入打粤语以便更好地学习粤语）：

諗住唔使用切割數組嘅方法來實現：
```go
/**
 * Definition for a binary tree node.
 * type TreeNode struct {
 *     Val int
 *     Left *TreeNode
 *     Right *TreeNode
 * }
 */
func buildTree(preorder []int, inorder []int) *TreeNode {
  var buildTree func(preOrderStart int, preOrderEnd int, inOrderStart int, inOrderEnd int) *TreeNode
  buildTree = func(preOrderStart int, preOrderEnd int, inOrderStart int, inOrderEnd int) *TreeNode {
    if (preOrderStart >= len(preorder) || inOrderStart >= len(inorder) || preOrderEnd - preOrderStart == 0 || inOrderEnd - inOrderStart == 0) {
      return nil
    }

    if (preOrderEnd - preOrderStart == 1 || inOrderEnd - inOrderStart == 1) {
      return &TreeNode{ Val: preorder[preOrderStart], Left: nil, Right: nil }
    }

    inOrderNodeIdx := findIndex(inorder, preorder[preOrderStart], inOrderStart, inOrderEnd)

    leftLen := inOrderNodeIdx - inOrderStart

    leftTree := buildTree(preOrderStart+1, preOrderStart + 1 + leftLen, inOrderStart, inOrderNodeIdx)

    rightTree := buildTree(preOrderStart + 1 + leftLen, preOrderEnd, inOrderNodeIdx + 1, inOrderEnd)

    return &TreeNode{
      Val: preorder[preOrderStart],
      Left: leftTree,
      Right: rightTree,
    }
  }

  return buildTree(0, len(preorder), 0, len(inorder))
}

func findIndex(s []int, e int, start int, end int) int {
  for i := start; i < end; i++ {
    if (s[i] == e) {
      return i
    }
  }
  return -1
}
```
要注意遞歸終止條件：
```go
 if (preOrderStart >= len(preorder) || inOrderStart >= len(inorder) || preOrderEnd - preOrderStart == 0 || inOrderEnd - inOrderStart == 0) {
      return nil
    }

    if (preOrderEnd - preOrderStart == 1 || inOrderEnd - inOrderStart == 1) {
      return &TreeNode{ Val: preorder[preOrderStart], Left: nil, Right: nil }
    }
```
分別系左子樹序列長度為 `0` （即喺左子樹為空）嘅時候同埋右子樹序列長度為 `0` （即喺右子樹為空）嘅時候，以及子樹長度為`1`嘅時候。

