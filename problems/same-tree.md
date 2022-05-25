
# 100. Same Tree - 相同的树

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Tree-树-blue.svg">   <img src="https://img.shields.io/badge/Depth-First Search-深度优先搜索-blue.svg">   <img src="https://img.shields.io/badge/Breadth-First Search-广度优先搜索-blue.svg">   <img src="https://img.shields.io/badge/Binary Tree-二叉树-blue.svg">  


## Description - 题目描述

### EN:
<p>Given the roots of two binary trees <code>p</code> and <code>q</code>, write a function to check if they are the same or not.</p>

<p>Two binary trees are considered the same if they are structurally identical, and the nodes have the same value.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2020/12/20/ex1.jpg" style="width: 622px; height: 182px;" />
<pre>
<strong>Input:</strong> p = [1,2,3], q = [1,2,3]
<strong>Output:</strong> true
</pre>

<p><strong>Example 2:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2020/12/20/ex2.jpg" style="width: 382px; height: 182px;" />
<pre>
<strong>Input:</strong> p = [1,2], q = [1,null,2]
<strong>Output:</strong> false
</pre>

<p><strong>Example 3:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2020/12/20/ex3.jpg" style="width: 622px; height: 182px;" />
<pre>
<strong>Input:</strong> p = [1,2,1], q = [1,1,2]
<strong>Output:</strong> false
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li>The number of nodes in both trees is in the range <code>[0, 100]</code>.</li>
	<li><code>-10<sup>4</sup> &lt;= Node.val &lt;= 10<sup>4</sup></code></li>
</ul>


### ZH-CN:
<p>给你两棵二叉树的根节点 <code>p</code> 和 <code>q</code> ，编写一个函数来检验这两棵树是否相同。</p>

<p>如果两个树在结构上相同，并且节点具有相同的值，则认为它们是相同的。</p>

<p> </p>

<p><strong>示例 1：</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2020/12/20/ex1.jpg" style="width: 622px; height: 182px;" />
<pre>
<strong>输入：</strong>p = [1,2,3], q = [1,2,3]
<strong>输出：</strong>true
</pre>

<p><strong>示例 2：</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2020/12/20/ex2.jpg" style="width: 382px; height: 182px;" />
<pre>
<strong>输入：</strong>p = [1,2], q = [1,null,2]
<strong>输出：</strong>false
</pre>

<p><strong>示例 3：</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2020/12/20/ex3.jpg" style="width: 622px; height: 182px;" />
<pre>
<strong>输入：</strong>p = [1,2,1], q = [1,1,2]
<strong>输出：</strong>false
</pre>

<p> </p>

<p><strong>提示：</strong></p>

<ul>
	<li>两棵树上的节点数目都在范围 <code>[0, 100]</code> 内</li>
	<li><code>-10<sup>4</sup> <= Node.val <= 10<sup>4</sup></code></li>
</ul>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/same-tree/description/)  -  [LeetCode-CN](https://leetcode-cn.com/problems/same-tree/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| javascript  | 52 ms | 10.5 MB | 2018/12/08 19:21 |

```javascript

/**
 * Definition for a binary tree node.
 * function TreeNode(val) {
 *     this.val = val;
 *     this.left = this.right = null;
 * }
 */
/**
 * @param {TreeNode} p
 * @param {TreeNode} q
 * @return {boolean}
 */


var isSameTree = function(p, q) {
    if (!p&&!q) {
        return true;
    } else if (!p&&q || !q&&p) {
        return false;
    }
    
    return (p.val === q.val && isSameTree(p.left, q.left) && isSameTree(p.right, q.right));
    
};

```
## My Notes - 我的笔记


## 100 相同的树

### 方法1 非递归

- 二叉树的非递归前序遍历
  - 根节点p不为空，打印，根节点入栈，并将左孩子作为当前节点，左孩子即当前节点不为空，打印。一个while搞定
  - 若左孩子为空，跳出while循环；if stack 不为空，top栈顶作为当前节点，pop栈顶，将当前节点的右孩子作为当前节点

``` javascript
/**
 * Definition for a binary tree node.
 * function TreeNode(val) {
 *     this.val = val;
 *     this.left = this.right = null;
 * }
 */
/**
 * @param {TreeNode} p
 * @param {TreeNode} q
 * @return {boolean}
 */

var isSameTree = function(p, q) {
    var cur1 = p, cur2 = q,
        stack1 = [], stack2 = [];
    // console.log(stack1.length);
    while ((cur1 || stack1.length !== 0) || (cur2 || stack2.length !== 0)) {
         if (!cur1 && !cur2 && stack1.length === stack2.length === 0) {
            return true;
        }
        
        while (cur1 || cur2) {
            if ((!cur1&&cur2) || (cur1&&!cur2)) {
                return false;
            }
            if (cur1.val === cur2.val) {
                stack1.push(cur1);
                stack2.push(cur2);
                cur1 = cur1.left;
                cur2 = cur2.left;
            } else {
                return false;
            }
        }
        
        if (stack1.length !== 0 || stack2.length !== 0) {
            if (stack1.length !== 0 && stack2.length !== 0) {
                cur1 = stack1.pop();
                cur2 = stack2.pop();
                cur1 = cur1.right;
                cur2 = cur2.right;
            } else if ((stack1.length === 0 && stack2.length !== 0) ||
                       (stack1.length !== 0 && stack2.length === 0)) {
                return false;
            }
        }
    }
    return true;
}
```

### 方法2 递归



```javascript
/**
 * Definition for a binary tree node.
 * function TreeNode(val) {
 *     this.val = val;
 *     this.left = this.right = null;
 * }
 */
/**
 * @param {TreeNode} p
 * @param {TreeNode} q
 * @return {boolean}
 */

var isSameTree = function(p, q) {
    if (!p&&!q) {
        return true;
    } else if (!p&&q || !q&&p) {
        return false;
    }
   
    return (p.val === q.val && isSameTree(p.left, q.left) && isSameTree(p.right, q.right)); //递归的返回值可以看作普通函数的返回值调用
    
};
```

