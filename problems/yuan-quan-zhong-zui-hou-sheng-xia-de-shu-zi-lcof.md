
# 剑指 Offer 62. 圆圈中最后剩下的数字 LCOF - 圆圈中最后剩下的数字

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Recursion-递归-blue.svg">   <img src="https://img.shields.io/badge/Math-数学-blue.svg">  


## Description - 题目描述

### EN:
<p>English description is not available for the problem. Please switch to Chinese.</p>


### ZH-CN:
<p>0,1,···,n-1这n个数字排成一个圆圈，从数字0开始，每次从这个圆圈里删除第m个数字（删除后从下一个数字开始计数）。求出这个圆圈里剩下的最后一个数字。</p>

<p>例如，0、1、2、3、4这5个数字组成一个圆圈，从数字0开始每次删除第3个数字，则删除的前4个数字依次是2、0、4、1，因此最后剩下的数字是3。</p>

<p> </p>

<p><strong>示例 1：</strong></p>

<pre>
<strong>输入:</strong> n = 5, m = 3
<strong>输出: </strong>3
</pre>

<p><strong>示例 2：</strong></p>

<pre>
<strong>输入:</strong> n = 10, m = 17
<strong>输出: </strong>2
</pre>

<p> </p>

<p><strong>限制：</strong></p>

<ul>
	<li><code>1 <= n <= 10^5</code></li>
	<li><code>1 <= m <= 10^6</code></li>
</ul>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/yuan-quan-zhong-zui-hou-sheng-xia-de-shu-zi-lcof/description/)  -  [LeetCode-CN](https://leetcode-cn.com/problems/yuan-quan-zhong-zui-hou-sheng-xia-de-shu-zi-lcof/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| typescript  | 72 ms | 42.2 MB | 2022/04/30 12:18 |

```typescript

function lastRemaining(n: number, m: number): number {
  if (n === 1) {
    return 0;
  }
  if (m === 1) {
    return n - 1;
  }

  let last = 0;

  for (let i = 2; i <= n; i++) {
    last = (last + m) % i;
  }

  return last;
};

```
## My Notes - 我的笔记


# 直接用环形链表方法做，超时
```typescript
class LinkNode {
  val: number = -1;
  next: LinkNode = null;
  constructor(val?: number) {
    this.val = val !== undefined ? val : -1;
    this.next = null;
  }
}

function lastRemaining(n: number, m: number): number {
  if (n === 1) {
    return 0;
  }

  if (m === 1) {
    return n - 1;
  }

  let start = new LinkNode(0);
  let cur = start;

  for (let i = 1; i < n; i++) {
    cur.next = new LinkNode(i);
    cur = cur.next;
  }

  cur.next = start;

  cur = start;


  let prev: LinkNode = null;

  let final = null;

  for (let i = 1; i < n; i++) {
    let counter = m - 1;
    while ( counter > 0 ) {
      if (counter === 1) {
        prev = cur;
      }
      cur = cur.next;
      counter--;
    }

    if (i === n - 1) {
      final = cur.next;
      cur.next = null;
      cur = null;
      break;
    }

    prev.next = cur.next;

    prev = cur.next;

    cur.next = null;

    cur = null;

    cur = prev;
  }

  return final.val;

};
```

用数学思路，有一个递推式，详见剑指 offer。

```typescript
function lastRemaining(n: number, m: number): number {
  if (n === 1) {
    return 0;
  }
  if (m === 1) {
    return n - 1;
  }

  let last = 0;

  for (let i = 2; i <= n; i++) {
    last = (last + m) % i;
  }

  return last;
};
```

