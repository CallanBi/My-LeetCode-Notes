
# 剑指 Offer 09. 用两个栈实现队列 LCOF - 用两个栈实现队列

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Stack-栈-blue.svg">   <img src="https://img.shields.io/badge/Design-设计-blue.svg">   <img src="https://img.shields.io/badge/Queue-队列-blue.svg">  


## Description - 题目描述

### EN:
English description is not available for the problem. Please switch to Chinese.

### ZH-CN:
<p>用两个栈实现一个队列。队列的声明如下，请实现它的两个函数 <code>appendTail</code> 和 <code>deleteHead</code> ，分别完成在队列尾部插入整数和在队列头部删除整数的功能。(若队列中没有元素，<code>deleteHead</code>&nbsp;操作返回 -1 )</p>

<p>&nbsp;</p>

<p><strong>示例 1：</strong></p>

<pre><strong>输入：</strong>
[&quot;CQueue&quot;,&quot;appendTail&quot;,&quot;deleteHead&quot;,&quot;deleteHead&quot;]
[[],[3],[],[]]
<strong>输出：</strong>[null,null,3,-1]
</pre>

<p><strong>示例 2：</strong></p>

<pre><strong>输入：</strong>
[&quot;CQueue&quot;,&quot;deleteHead&quot;,&quot;appendTail&quot;,&quot;appendTail&quot;,&quot;deleteHead&quot;,&quot;deleteHead&quot;]
[[],[],[5],[2],[],[]]
<strong>输出：</strong>[null,-1,null,null,5,2]
</pre>

<p><strong>提示：</strong></p>

<ul>
	<li><code>1 &lt;= values &lt;= 10000</code></li>
	<li><code>最多会对&nbsp;appendTail、deleteHead 进行&nbsp;10000&nbsp;次调用</code></li>
</ul>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/yong-liang-ge-zhan-shi-xian-dui-lie-lcof/description/)  -  [LeetCode-CN](https://leetcode-cn.com/problems/yong-liang-ge-zhan-shi-xian-dui-lie-lcof/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| typescript  | 404 ms | 50.3 MB | 2021/04/04 17:22 |

```typescript

class CQueue<T> {
  private _stack1: Array<T>;
  private _stack2: Array<T>;
  constructor() {
    this._stack1 = [];
    this._stack2 = [];
  }

  public appendTail = (value: T): void => {
    this._stack1.push(value);
  }

  public deleteHead: () => T | -1 = () => {
    const len = this._stack1.length;
    if (len > 0 && this._stack2.length === 0) {
      for (let i = 0; i < len; i++) {
        const e = this._stack1.pop();
        this._stack2.push(e);
      }
    }
    if (this._stack2.length === 0) {
      return -1;
    } else {
     return this._stack2.pop();
    }
  }
}

/**
 * Your CQueue object will be instantiated and called as such:
 * var obj = new CQueue()
 * obj.appendTail(value)
 * var param_2 = obj.deleteHead()
 */

```
## My Notes - 我的笔记


1. 要注意当 stack2 里什么都没有时stack1才出栈，不然就违反先进先出了
2. stack1的 length 在 pop后会变化，如果写 for循环要先保存下来，写 while 则不用
3. 类的泛型在类后加一个`<T>`；`pravite`声明在先，只写类型，constructor再赋值

