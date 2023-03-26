
# 297. Serialize and Deserialize Binary Tree - 二叉树的序列化与反序列化

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Tree-树-blue.svg">   <img src="https://img.shields.io/badge/Depth First Search-深度优先搜索-blue.svg">   <img src="https://img.shields.io/badge/Breadth First Search-广度优先搜索-blue.svg">   <img src="https://img.shields.io/badge/Design-设计-blue.svg">   <img src="https://img.shields.io/badge/String-字符串-blue.svg">   <img src="https://img.shields.io/badge/Binary Tree-二叉树-blue.svg">  


## Description - 题目描述

### EN:
<p>Serialization is the process of converting a data structure or object into a sequence of bits so that it can be stored in a file or memory buffer, or transmitted across a network connection link to be reconstructed later in the same or another computer environment.</p>

<p>Design an algorithm to serialize and deserialize a binary tree. There is no restriction on how your serialization/deserialization algorithm should work. You just need to ensure that a binary tree can be serialized to a string and this string can be deserialized to the original tree structure.</p>

<p><strong>Clarification:</strong> The input/output format is the same as <a href="https://support.leetcode.com/hc/en-us/articles/360011883654-What-does-1-null-2-3-mean-in-binary-tree-representation-" target="_blank">how LeetCode serializes a binary tree</a>. You do not necessarily need to follow this format, so please be creative and come up with different approaches yourself.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2020/09/15/serdeser.jpg" style="width: 442px; height: 324px;" />
<pre>
<strong>Input:</strong> root = [1,2,3,null,null,4,5]
<strong>Output:</strong> [1,2,3,null,null,4,5]
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre>
<strong>Input:</strong> root = []
<strong>Output:</strong> []
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li>The number of nodes in the tree is in the range <code>[0, 10<sup>4</sup>]</code>.</li>
	<li><code>-1000 &lt;= Node.val &lt;= 1000</code></li>
</ul>


### ZH-CN:
<p>序列化是将一个数据结构或者对象转换为连续的比特位的操作，进而可以将转换后的数据存储在一个文件或者内存中，同时也可以通过网络传输到另一个计算机环境，采取相反方式重构得到原数据。</p>

<p>请设计一个算法来实现二叉树的序列化与反序列化。这里不限定你的序列 / 反序列化算法执行逻辑，你只需要保证一个二叉树可以被序列化为一个字符串并且将这个字符串反序列化为原始的树结构。</p>

<p><strong>提示: </strong>输入输出格式与 LeetCode 目前使用的方式一致，详情请参阅 <a href="/faq/#binary-tree">LeetCode 序列化二叉树的格式</a>。你并非必须采取这种方式，你也可以采用其他的方法解决这个问题。</p>

<p> </p>

<p><strong>示例 1：</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2020/09/15/serdeser.jpg" style="width: 442px; height: 324px;" />
<pre>
<strong>输入：</strong>root = [1,2,3,null,null,4,5]
<strong>输出：</strong>[1,2,3,null,null,4,5]
</pre>

<p><strong>示例 2：</strong></p>

<pre>
<strong>输入：</strong>root = []
<strong>输出：</strong>[]
</pre>

<p><strong>示例 3：</strong></p>

<pre>
<strong>输入：</strong>root = [1]
<strong>输出：</strong>[1]
</pre>

<p><strong>示例 4：</strong></p>

<pre>
<strong>输入：</strong>root = [1,2]
<strong>输出：</strong>[1,2]
</pre>

<p> </p>

<p><strong>提示：</strong></p>

<ul>
	<li>树中结点数在范围 <code>[0, 10<sup>4</sup>]</code> 内</li>
	<li><code>-1000 <= Node.val <= 1000</code></li>
</ul>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/serialize-and-deserialize-binary-tree/description/)  -  [LeetCode-CN](https://leetcode.cn/problems/serialize-and-deserialize-binary-tree/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| typescript  | 112 ms | 54.2 MB | 2023/03/26 16:07 |

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

/*
 * Encodes a tree to a single string.
 */
function serialize(root: TreeNode | null): string {
  if (root === null) {
    return '[]';
  }

  const ans: string[] = [];

  const queue: TreeNode[] = [];

  queue.push(root);

  let queuePtr = 0;

  let node = queue[queuePtr++];

  ans.push(node.val.toString());

  queue.push(node.left);
  queue.push(node.right);

  while (queuePtr < queue.length) {
    node = queue[queuePtr++];

    if (node === null) {
      ans.push('null');
      continue;
    } else {
      ans.push(node.val.toString());
    }
    queue.push(node.left);
    queue.push(node.right);
  }

  return `[${ans.join(',')}]`

};

/*
 * Decodes your encoded data to tree.
 */
function deserialize(data: string): TreeNode | null {
  if (data === '[]') {
    return null;
  }

  const arr: string[] = data.slice(1, data.length - 1).split(',');

  if (arr.length === 0) {
    return null;
  }


  let arrPtr = 0, queuePtr = 0;

  const queue: TreeNode[] = [];

  const root: TreeNode = new TreeNode(Number(arr[arrPtr++]));

  queue.push(root);

  let curNode = null;

  while (arrPtr < arr.length && queuePtr < queue.length) {
    curNode = queue[queuePtr++];
    const leftStr = arr[arrPtr++];
    const rightStr = arr[arrPtr++];

    if (leftStr !== 'null') {
      curNode.left = new TreeNode(Number(leftStr));
    }

    if (rightStr !== 'null') {
      curNode.right = new TreeNode(Number(rightStr));
    }

    if (curNode.left !== null) {
      queue.push(curNode.left);

    }

    if (curNode.right !== null) {
      queue.push(curNode.right);
    }
  }


  return root;
};


/**
 * Your functions will be called as such:
 * deserialize(serialize(root));
 */

```
## My Notes - 我的笔记


最开始想到用层序遍历的队列去做：
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

/*
 * Encodes a tree to a single string.
 */
function serialize(root: TreeNode | null): string {
  if (root === null) {
    return '[]';
  }

  const ans: string[] = [];

  const queue: TreeNode[] = [];

  queue.push(root);

  let node = queue.shift();

  ans.push(node.val.toString());

  queue.push(node.left)
  queue.push(node.right)

  while (queue.length > 0) {
    node = queue.shift();

    if (node === null) {
      ans.push('null');
      continue;
    } else {
      ans.push(node.val.toString());
    }
    queue.push(node.left);
    queue.push(node.right);
  }

  return `[${ans.join(',')}]`

};

/*
 * Decodes your encoded data to tree.
 */
function deserialize(data: string): TreeNode | null {
  if (data === '[]') {
    return null;
  }

  const arr: string[] = data.slice(1, data.length - 1).split(',');

  if (arr.length === 0) {
    return null;
  }

  const queue: TreeNode[] = [];

  const root: TreeNode = new TreeNode(Number(arr.shift()));

  queue.push(root);

  let curNode = null;

  while (queue.length > 0 && arr.length > 0) {
    curNode = queue.shift();
    const leftStr = arr.shift();
    const rightStr = arr.shift();

    if (leftStr !== 'null') {
      curNode.left = new TreeNode(Number(leftStr));
    }

    if (rightStr !== 'null') {
      curNode.right = new TreeNode(Number(rightStr));
    }

    if (curNode.left !== null) {
      queue.push(curNode.left);

    }

    if (curNode.right !== null) {
      queue.push(curNode.right);
    }
  }


  return root;
};


/**
 * Your functions will be called as such:
 * deserialize(serialize(root));
 */
```

由于 shift 的时间复杂度为 $O(n)$，AC 后花了1292ms，时间复杂度只击败了5%，所以考虑用指针去优化。
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

/*
 * Encodes a tree to a single string.
 */
function serialize(root: TreeNode | null): string {
  if (root === null) {
    return '[]';
  }

  const ans: string[] = [];

  const queue: TreeNode[] = [];

  queue.push(root);

  let queuePtr = 0;

  let node = queue[queuePtr++];

  ans.push(node.val.toString());

  queue.push(node.left);
  queue.push(node.right);

  while (queuePtr < queue.length) {
    node = queue[queuePtr++];

    if (node === null) {
      ans.push('null');
      continue;
    } else {
      ans.push(node.val.toString());
    }
    queue.push(node.left);
    queue.push(node.right);
  }

  return `[${ans.join(',')}]`

};

/*
 * Decodes your encoded data to tree.
 */
function deserialize(data: string): TreeNode | null {
  if (data === '[]') {
    return null;
  }

  const arr: string[] = data.slice(1, data.length - 1).split(',');

  if (arr.length === 0) {
    return null;
  }


  let arrPtr = 0, queuePtr = 0;

  const queue: TreeNode[] = [];

  const root: TreeNode = new TreeNode(Number(arr[arrPtr++]));

  queue.push(root);

  let curNode = null;

  while (arrPtr < arr.length && queuePtr < queue.length) {
    curNode = queue[queuePtr++];
    const leftStr = arr[arrPtr++];
    const rightStr = arr[arrPtr++];

    if (leftStr !== 'null') {
      curNode.left = new TreeNode(Number(leftStr));
    }

    if (rightStr !== 'null') {
      curNode.right = new TreeNode(Number(rightStr));
    }

    if (curNode.left !== null) {
      queue.push(curNode.left);

    }

    if (curNode.right !== null) {
      queue.push(curNode.right);
    }
  }


  return root;
};


/**
 * Your functions will be called as such:
 * deserialize(serialize(root));
 */
```

优化后花了112ms，时间复杂度击败了75%。

