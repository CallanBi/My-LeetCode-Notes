
# 剑指 Offer 59 - II. 队列的最大值 LCOF - 队列的最大值

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Design-设计-blue.svg">   <img src="https://img.shields.io/badge/Queue-队列-blue.svg">   <img src="https://img.shields.io/badge/Monotonic Queue-单调队列-blue.svg">  


## Description - 题目描述

### EN:
<p>English description is not available for the problem. Please switch to Chinese.</p>

### ZH-CN:
<p>请定义一个队列并实现函数 <code>max_value</code> 得到队列里的最大值，要求函数<code>max_value</code>、<code>push_back</code> 和 <code>pop_front</code> 的<strong>均摊</strong>时间复杂度都是O(1)。</p>

<p>若队列为空，<code>pop_front</code> 和 <code>max_value</code>&nbsp;需要返回 -1</p>

<p><strong>示例 1：</strong></p>

<pre><strong>输入:</strong> 
[&quot;MaxQueue&quot;,&quot;push_back&quot;,&quot;push_back&quot;,&quot;max_value&quot;,&quot;pop_front&quot;,&quot;max_value&quot;]
[[],[1],[2],[],[],[]]
<strong>输出:&nbsp;</strong>[null,null,null,2,1,2]
</pre>

<p><strong>示例 2：</strong></p>

<pre><strong>输入:</strong> 
[&quot;MaxQueue&quot;,&quot;pop_front&quot;,&quot;max_value&quot;]
[[],[],[]]
<strong>输出:&nbsp;</strong>[null,-1,-1]
</pre>

<p>&nbsp;</p>

<p><strong>限制：</strong></p>

<ul>
	<li><code>1 &lt;= push_back,pop_front,max_value的总操作数&nbsp;&lt;= 10000</code></li>
	<li><code>1 &lt;= value &lt;= 10^5</code></li>
</ul>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/dui-lie-de-zui-da-zhi-lcof/description/)  -  [LeetCode-CN](https://leetcode.cn/problems/dui-lie-de-zui-da-zhi-lcof/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| typescript  | 188 ms | 51.7 MB | 2022/04/23 19:54 |

```typescript

class MaxQueue {
    static queue: number[] = [];
    static monoQueue: number[] = [];
    constructor() {
      MaxQueue.queue = [];
      MaxQueue.monoQueue = [];
    }

    max_value(): number {
      if (MaxQueue.queue.length === 0) {
        return -1;
      }

      return MaxQueue.monoQueue[0];
    }

    push_back(value: number): void {
      MaxQueue.queue.push(value);

      while (MaxQueue.monoQueue[MaxQueue.monoQueue.length - 1] !== undefined && MaxQueue.monoQueue[MaxQueue.monoQueue.length - 1] < value) {
        MaxQueue.monoQueue.pop();
      }

      MaxQueue.monoQueue.push(value);
    }

    pop_front(): number {
      const top = MaxQueue.queue.shift();
      if (MaxQueue.monoQueue[0] === top) {
        MaxQueue.monoQueue.shift();
      }
      return top === undefined ? -1 : top;
    }
}

/**
 * Your MaxQueue object will be instantiated and called as such:
 * var obj = new MaxQueue()
 * var param_1 = obj.max_value()
 * obj.push_back(value)
 * var param_3 = obj.pop_front()
 */

```
## My Notes - 我的笔记


与 剑指 Offer 59 - I: 滑动窗口的最大值 思路一致。

