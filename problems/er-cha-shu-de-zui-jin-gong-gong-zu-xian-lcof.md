
# 剑指 Offer 68 - II. 二叉树的最近公共祖先 LCOF - 二叉树的最近公共祖先

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Tree-树-blue.svg">   <img src="https://img.shields.io/badge/Depth First Search-深度优先搜索-blue.svg">   <img src="https://img.shields.io/badge/Binary Tree-二叉树-blue.svg">  


## Description - 题目描述

### EN:
<p>English description is not available for the problem. Please switch to Chinese.</p>


### ZH-CN:
<p>给定一个二叉树, 找到该树中两个指定节点的最近公共祖先。</p>

<p><a href="https://baike.baidu.com/item/%E6%9C%80%E8%BF%91%E5%85%AC%E5%85%B1%E7%A5%96%E5%85%88/8918834?fr=aladdin" target="_blank">百度百科</a>中最近公共祖先的定义为：&ldquo;对于有根树 T 的两个结点 p、q，最近公共祖先表示为一个结点 x，满足 x 是 p、q 的祖先且 x 的深度尽可能大（<strong>一个节点也可以是它自己的祖先</strong>）。&rdquo;</p>

<p>例如，给定如下二叉树:&nbsp; root =&nbsp;[3,5,1,6,2,0,8,null,null,7,4]</p>

<p><img alt="" src="https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2018/12/15/binarytree.png"></p>

<p>&nbsp;</p>

<p><strong>示例 1:</strong></p>

<pre><strong>输入:</strong> root = [3,5,1,6,2,0,8,null,null,7,4], p = 5, q = 1
<strong>输出:</strong> 3
<strong>解释: </strong>节点 <code>5 </code>和节点 <code>1 </code>的最近公共祖先是节点 <code>3。</code>
</pre>

<p><strong>示例&nbsp;2:</strong></p>

<pre><strong>输入:</strong> root = [3,5,1,6,2,0,8,null,null,7,4], p = 5, q = 4
<strong>输出:</strong> 5
<strong>解释: </strong>节点 <code>5 </code>和节点 <code>4 </code>的最近公共祖先是节点 <code>5。</code>因为根据定义最近公共祖先节点可以为节点本身。
</pre>

<p>&nbsp;</p>

<p><strong>说明:</strong></p>

<ul>
	<li>所有节点的值都是唯一的。</li>
	<li>p、q 为不同节点且均存在于给定的二叉树中。</li>
</ul>

<p>注意：本题与主站 236 题相同：<a href="https://leetcode-cn.com/problems/lowest-common-ancestor-of-a-binary-tree/">https://leetcode-cn.com/problems/lowest-common-ancestor-of-a-binary-tree/</a></p>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/er-cha-shu-de-zui-jin-gong-gong-zu-xian-lcof/description/)  -  [LeetCode-CN](https://leetcode.cn/problems/er-cha-shu-de-zui-jin-gong-gong-zu-xian-lcof/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| typescript  | 76 ms | 51.5 MB | 2022/04/30 17:59 |

```typescript

/**
 * Definition for a binary tree node.
 * class TreeNode {
 *     val: number
 *     left: TreeNode | null
 *     right: TreeNode | null
 *     constructor(val?: number, left?: TreeNode | null, right?: TreeNode | null) {
 *         this.val = (val===undefined ? 0 : val)
 *         this.left = (left===undefined ? null : left)
 *         this.right = (right===undefined ? null : right)
 *     }
 * }
 */
function lowestCommonAncestor(root: TreeNode | null, p: TreeNode | null, q: TreeNode | null): TreeNode | null {
  if (!p || !q || !root) {
    return null;
  }

	if (p.val === root.val || q.val === root.val) {
    return root;
  } 

  const left = lowestCommonAncestor(root.left, p, q);

  const right = lowestCommonAncestor(root.right, p, q);

  if (left && right) {
    return root;
  } else {
    return left ?? right ?? null;
  }
};

```
## My Notes - 我的笔记


我的想法：

一个递归。

递归里判断左右子树是否有一个输入的节点在子树里面，有则返回该节点。

如果左右都有，则当前节点是最大公共结点，直接返回。

如果只有左边有或者只有右边有，则返回有的那个节点。

如果都没有，则返回 `null `。

```typescript
/**
 * Definition for a binary tree node.
 * class TreeNode {
 *     val: number
 *     left: TreeNode | null
 *     right: TreeNode | null
 *     constructor(val?: number, left?: TreeNode | null, right?: TreeNode | null) {
 *         this.val = (val===undefined ? 0 : val)
 *         this.left = (left===undefined ? null : left)
 *         this.right = (right===undefined ? null : right)
 *     }
 * }
 */
function lowestCommonAncestor(root: TreeNode | null, p: TreeNode | null, q: TreeNode | null): TreeNode | null {
  if (!p || !q || !root) {
    return null;
  }

	if (p.val === root.val || q.val === root.val) {
    return root;
  } 

  const left = lowestCommonAncestor(root.left, p, q);

  const right = lowestCommonAncestor(root.right, p, q);

  if (left && right) {
    return root;
  } else {
    return left ?? right ?? null;
  }
};
```

