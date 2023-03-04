
# 155. Min Stack - 最小栈

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Stack-栈-blue.svg">   <img src="https://img.shields.io/badge/Design-设计-blue.svg">  


## Description - 题目描述

### EN:
<p>Design a stack that supports push, pop, top, and retrieving the minimum element in constant time.</p>

<p>Implement the <code>MinStack</code> class:</p>

<ul>
	<li><code>MinStack()</code> initializes the stack object.</li>
	<li><code>void push(int val)</code> pushes the element <code>val</code> onto the stack.</li>
	<li><code>void pop()</code> removes the element on the top of the stack.</li>
	<li><code>int top()</code> gets the top element of the stack.</li>
	<li><code>int getMin()</code> retrieves the minimum element in the stack.</li>
</ul>

<p>You must implement a solution with <code>O(1)</code> time complexity for each function.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input</strong>
[&quot;MinStack&quot;,&quot;push&quot;,&quot;push&quot;,&quot;push&quot;,&quot;getMin&quot;,&quot;pop&quot;,&quot;top&quot;,&quot;getMin&quot;]
[[],[-2],[0],[-3],[],[],[],[]]

<strong>Output</strong>
[null,null,null,null,-3,null,0,-2]

<strong>Explanation</strong>
MinStack minStack = new MinStack();
minStack.push(-2);
minStack.push(0);
minStack.push(-3);
minStack.getMin(); // return -3
minStack.pop();
minStack.top();    // return 0
minStack.getMin(); // return -2
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>-2<sup>31</sup> &lt;= val &lt;= 2<sup>31</sup> - 1</code></li>
	<li>Methods <code>pop</code>, <code>top</code> and <code>getMin</code> operations will always be called on <strong>non-empty</strong> stacks.</li>
	<li>At most <code>3 * 10<sup>4</sup></code> calls will be made to <code>push</code>, <code>pop</code>, <code>top</code>, and <code>getMin</code>.</li>
</ul>


### ZH-CN:
<p>设计一个支持 <code>push</code> ，<code>pop</code> ，<code>top</code> 操作，并能在常数时间内检索到最小元素的栈。</p>

<p>实现 <code>MinStack</code> 类:</p>

<ul>
	<li><code>MinStack()</code> 初始化堆栈对象。</li>
	<li><code>void push(int val)</code> 将元素val推入堆栈。</li>
	<li><code>void pop()</code> 删除堆栈顶部的元素。</li>
	<li><code>int top()</code> 获取堆栈顶部的元素。</li>
	<li><code>int getMin()</code> 获取堆栈中的最小元素。</li>
</ul>

<p>&nbsp;</p>

<p><strong>示例 1:</strong></p>

<pre>
<strong>输入：</strong>
["MinStack","push","push","push","getMin","pop","top","getMin"]
[[],[-2],[0],[-3],[],[],[],[]]

<strong>输出：</strong>
[null,null,null,null,-3,null,0,-2]

<strong>解释：</strong>
MinStack minStack = new MinStack();
minStack.push(-2);
minStack.push(0);
minStack.push(-3);
minStack.getMin();   --&gt; 返回 -3.
minStack.pop();
minStack.top();      --&gt; 返回 0.
minStack.getMin();   --&gt; 返回 -2.
</pre>

<p>&nbsp;</p>

<p><strong>提示：</strong></p>

<ul>
	<li><code>-2<sup>31</sup>&nbsp;&lt;= val &lt;= 2<sup>31</sup>&nbsp;- 1</code></li>
	<li><code>pop</code>、<code>top</code> 和 <code>getMin</code> 操作总是在 <strong>非空栈</strong> 上调用</li>
	<li><code>push</code>,&nbsp;<code>pop</code>,&nbsp;<code>top</code>, and&nbsp;<code>getMin</code>最多被调用&nbsp;<code>3 * 10<sup>4</sup></code>&nbsp;次</li>
</ul>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/min-stack/description/)  -  [LeetCode-CN](https://leetcode.cn/problems/min-stack/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| typescript  | 112 ms | 51.3 MB | 2023/03/04 22:03 |

```typescript

type StackItem = {
  value: number;
  minVal: number;
}

class MinStack {
  private _stack: StackItem[];
  private _min: number;

  constructor() {
    this._stack = [];
    this._min = +Infinity;
  }

  push(val: number): void {
    if (this._min > val) {
      this._min = val;
    }
    this._stack.push({
      value: val,
      minVal: this._min
    });
  }

  pop(): void {
    this._stack.pop();
    if (this._stack.length !== 0) {
      this._min = this._stack[this._stack.length - 1].minVal;
    } else {
      this._min = +Infinity;
    }
  }

  top(): number {
    return this._stack[this._stack.length - 1].value;
  }

  getMin(): number {
    return this._stack[this._stack.length - 1].minVal;
  }
}

/**
 * Your MinStack object will be instantiated and called as such:
 * var obj = new MinStack()
 * obj.push(val)
 * obj.pop()
 * var param_3 = obj.top()
 * var param_4 = obj.getMin()
 */

```
## My Notes - 我的笔记


stackItem 保存一个入栈时的最小值状态即可。
```typescript
type StackItem = {
  value: number;
  minVal: number;
}

class MinStack {
  private _stack: StackItem[];
  private _min: number;

  constructor() {
    this._stack = [];
    this._min = +Infinity;
  }

  push(val: number): void {
    if (this._min > val) {
      this._min = val;
    }
    this._stack.push({
      value: val,
      minVal: this._min
    });
  }

  pop(): void {
    this._stack.pop();
    if (this._stack.length !== 0) {
      this._min = this._stack[this._stack.length - 1].minVal;
    } else {
      this._min = +Infinity;
    }
  }

  top(): number {
    return this._stack[this._stack.length - 1].value;
  }

  getMin(): number {
    return this._stack[this._stack.length - 1].minVal;
  }
}

/**
 * Your MinStack object will be instantiated and called as such:
 * var obj = new MinStack()
 * obj.push(val)
 * obj.pop()
 * var param_3 = obj.top()
 * var param_4 = obj.getMin()
 */
```
注意： 栈清空时，需要重新把全局最小值设为`+Infinity`。

