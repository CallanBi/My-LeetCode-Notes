
# 剑指 Offer 18. 删除链表的节点 LCOF - 删除链表的节点

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Linked List-链表-blue.svg">  


## Description - 题目描述

### EN:
English description is not available for the problem. Please switch to Chinese.

### ZH-CN:
<p>给定单向链表的头指针和一个要删除的节点的值，定义一个函数删除该节点。</p>

<p>返回删除后的链表的头节点。</p>

<p><strong>注意：</strong>此题对比原题有改动</p>

<p><strong>示例 1:</strong></p>

<pre><strong>输入:</strong> head = [4,5,1,9], val = 5
<strong>输出:</strong> [4,1,9]
<strong>解释: </strong>给定你链表中值为&nbsp;5&nbsp;的第二个节点，那么在调用了你的函数之后，该链表应变为 4 -&gt; 1 -&gt; 9.
</pre>

<p><strong>示例 2:</strong></p>

<pre><strong>输入:</strong> head = [4,5,1,9], val = 1
<strong>输出:</strong> [4,5,9]
<strong>解释: </strong>给定你链表中值为&nbsp;1&nbsp;的第三个节点，那么在调用了你的函数之后，该链表应变为 4 -&gt; 5 -&gt; 9.
</pre>

<p>&nbsp;</p>

<p><strong>说明：</strong></p>

<ul>
	<li>题目保证链表中节点的值互不相同</li>
	<li>若使用 C 或 C++ 语言，你不需要 <code>free</code> 或 <code>delete</code> 被删除的节点</li>
</ul>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/shan-chu-lian-biao-de-jie-dian-lcof/description/)  -  [LeetCode-CN](https://leetcode.cn/problems/shan-chu-lian-biao-de-jie-dian-lcof/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| typescript  | 96 ms | 39.9 MB | 2021/05/01 16:41 |

```typescript

/**
 * Definition for singly-linked list.
 * class ListNode {
 *     val: number
 *     next: ListNode | null
 *     constructor(val?: number, next?: ListNode | null) {
 *         this.val = (val===undefined ? 0 : val)
 *         this.next = (next===undefined ? null : next)
 *     }
 * }
 */

function deleteNode(head: ListNode | null, val: number): ListNode | null {
    if (!head) {
        return null;
    }
    let cur = head;
    let prev = null;
    while (cur) {
        if (val === cur.val) {
            if (!prev) {
                // 是头结点
                return cur.next || null;
            } else {
                prev.next = cur.next || null;
                cur = null;
                break;
            }
        } else {
            prev = cur;
            cur = cur.next
        }
    }
    return head;
};

```
## My Notes - 我的笔记


循环条件不是`while(cur.next)` 否则到最后一个节点就不执行了

