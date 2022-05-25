
# 剑指 Offer 30. 包含min函数的栈 LCOF - 包含min函数的栈

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Stack-栈-blue.svg">   <img src="https://img.shields.io/badge/Design-设计-blue.svg">  


## Description - 题目描述

### EN:
English description is not available for the problem. Please switch to Chinese.

### ZH-CN:
<p>定义栈的数据结构，请在该类型中实现一个能够得到栈的最小元素的 min 函数在该栈中，调用 min、push 及 pop 的时间复杂度都是 O(1)。</p>

<p>&nbsp;</p>

<p><strong>示例:</strong></p>

<pre>MinStack minStack = new MinStack();
minStack.push(-2);
minStack.push(0);
minStack.push(-3);
minStack.min();   --&gt; 返回 -3.
minStack.pop();
minStack.top();      --&gt; 返回 0.
minStack.min();   --&gt; 返回 -2.
</pre>

<p>&nbsp;</p>

<p><strong>提示：</strong></p>

<ol>
	<li>各函数的调用总次数不超过 20000 次</li>
</ol>

<p>&nbsp;</p>

<p>注意：本题与主站 155 题相同：<a href="https://leetcode-cn.com/problems/min-stack/">https://leetcode-cn.com/problems/min-stack/</a></p>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/bao-han-minhan-shu-de-zhan-lcof/description/)  -  [LeetCode-CN](https://leetcode-cn.com/problems/bao-han-minhan-shu-de-zhan-lcof/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| typescript  | 124 ms | 47 MB | 2021/11/07 18:30 |

```typescript

class MinStack {
  private stack: number[];
  private assitantStack: number[];

  constructor() {
    this.stack = [];
    this.assitantStack = [];
  }

  push(x: number): void {
    this.stack.push(x);
    if (this.assitantStack.length > 0) {
      const assitantTop = this.assitantStack[this.assitantStack.length-1];
      if (x < assitantTop) {
        this.assitantStack.push(x);
      } else {
        this.assitantStack.push(assitantTop);
      }
    } else {
      this.assitantStack.push(x);
    }
  }

  pop(): void {
    this.stack.pop();
    this.assitantStack.pop();
  }

  top(): number {
    return this.stack[this.stack.length-1];
  }

  min(): number {
    return this.assitantStack[this.assitantStack.length-1];
  }
}

/**
 * Your MinStack object will be instantiated and called as such:
 * var obj = new MinStack()
 * obj.push(x)
 * obj.pop()
 * var param_3 = obj.top()
 * var param_4 = obj.min()
 */

```
## My Notes - 我的笔记


剑指 offer 里的辅助栈思路。
```typescript
class MinStack {
  private stack: number[];
  private assitantStack: number[];

  constructor() {
    this.stack = [];
    this.assitantStack = [];
  }

  push(x: number): void {
    this.stack.push(x);
    if (this.assitantStack.length > 0) {
      const assitantTop = this.assitantStack[this.assitantStack.length-1];
      if (x < assitantTop) {
        this.assitantStack.push(x);
      } else {
        // 不大于栈中的任何一个元素时，还是得将辅助栈的 top 再压入一遍，这样才保证出栈时最小值是正确的
        this.assitantStack.push(assitantTop);
      }
    } else {
      this.assitantStack.push(x);
    }
  }

  pop(): void {
    this.stack.pop();
    this.assitantStack.pop();
  }

  top(): number {
    return this.stack[this.stack.length-1];
  }

  min(): number {
    return this.assitantStack[this.assitantStack.length-1];
  }
}

/**
 * Your MinStack object will be instantiated and called as such:
 * var obj = new MinStack()
 * obj.push(x)
 * obj.pop()
 * var param_3 = obj.top()
 * var param_4 = obj.min()
 */
```

