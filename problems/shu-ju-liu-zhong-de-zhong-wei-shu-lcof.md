
# 剑指 Offer 41. 数据流中的中位数  LCOF - 数据流中的中位数

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Design-设计-blue.svg">   <img src="https://img.shields.io/badge/Two Pointers-双指针-blue.svg">   <img src="https://img.shields.io/badge/Data Stream-数据流-blue.svg">   <img src="https://img.shields.io/badge/Sorting-排序-blue.svg">   <img src="https://img.shields.io/badge/Heap (Priority Queue)-堆（优先队列）-blue.svg">  


## Description - 题目描述

### EN:
English description is not available for the problem. Please switch to Chinese.

### ZH-CN:
<p>如何得到一个数据流中的中位数？如果从数据流中读出奇数个数值，那么中位数就是所有数值排序之后位于中间的数值。如果从数据流中读出偶数个数值，那么中位数就是所有数值排序之后中间两个数的平均值。</p>

<p>例如，</p>

<p>[2,3,4]&nbsp;的中位数是 3</p>

<p>[2,3] 的中位数是 (2 + 3) / 2 = 2.5</p>

<p>设计一个支持以下两种操作的数据结构：</p>

<ul>
	<li>void addNum(int num) - 从数据流中添加一个整数到数据结构中。</li>
	<li>double findMedian() - 返回目前所有元素的中位数。</li>
</ul>

<p><strong>示例 1：</strong></p>

<pre><strong>输入：
</strong>[&quot;MedianFinder&quot;,&quot;addNum&quot;,&quot;addNum&quot;,&quot;findMedian&quot;,&quot;addNum&quot;,&quot;findMedian&quot;]
[[],[1],[2],[],[3],[]]
<strong>输出：</strong>[null,null,null,1.50000,null,2.00000]
</pre>

<p><strong>示例 2：</strong></p>

<pre><strong>输入：
</strong>[&quot;MedianFinder&quot;,&quot;addNum&quot;,&quot;findMedian&quot;,&quot;addNum&quot;,&quot;findMedian&quot;]
[[],[2],[],[3],[]]
<strong>输出：</strong>[null,null,2.00000,null,2.50000]</pre>

<p>&nbsp;</p>

<p><strong>限制：</strong></p>

<ul>
	<li>最多会对&nbsp;<code>addNum、findMedian</code> 进行&nbsp;<code>50000</code>&nbsp;次调用。</li>
</ul>

<p>注意：本题与主站 295 题相同：<a href="https://leetcode-cn.com/problems/find-median-from-data-stream/">https://leetcode-cn.com/problems/find-median-from-data-stream/</a></p>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/shu-ju-liu-zhong-de-zhong-wei-shu-lcof/description/)  -  [LeetCode-CN](https://leetcode.cn/problems/shu-ju-liu-zhong-de-zhong-wei-shu-lcof/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| javascript  | 260 ms | 58.9 MB | 2021/12/10 14:16 |

```javascript

class MedianFinder {
  // static 不能在类的实例上用
  static _minHeap; 
  static _maxHeap;
  static _counter;
  constructor() {
    this._maxHeap = new MaxPriorityQueue(); // 左边
    this._minHeap = new MinPriorityQueue(); // 右边
    this._counter = 0;
  }

  addNum(num) {
    this._counter++;
    if (this._counter % 2 === 1) { // 奇数，想放左边
      if (this._minHeap.front() !== null) {
        if (num >= this._minHeap.front().element) {
          const minTop = this._minHeap.dequeue().element;
          this._maxHeap.enqueue(minTop);
          this._minHeap.enqueue(num);
        } else {
          this._maxHeap.enqueue(num);
        }
      } else {
        this._maxHeap.enqueue(num);
      }
    } else {
      if (this._maxHeap.front() !== null) {
        if (num <= this._maxHeap.front().element) {
          const maxTop = this._maxHeap.dequeue().element;
          this._minHeap.enqueue(maxTop);
          this._maxHeap.enqueue(num);
        } else {
          this._minHeap.enqueue(num);
        }
      } else {
        this._minHeap.enqueue(num);
      }
    }
  }

  findMedian() {
    if (this._maxHeap.size() === this._minHeap.size()) {
      return (this._maxHeap.front().element + this._minHeap.front().element) / 2;
    } else {
      return this._maxHeap.size() > this._minHeap.size() ? this._maxHeap.front().element : this._minHeap.front().element;
    }
  }
}

/**
 * Your MedianFinder object will be instantiated and called as such:
 * var obj = new MedianFinder()
 * obj.addNum(num)
 * var param_2 = obj.findMedian()
 */

```
## My Notes - 我的笔记


堆的典型应用。直接用优先队列模拟堆。

思路：

初始化一个最大堆，一个最小堆。最大堆用来保存数据流中小的部分，位于排序的数据流中的左半部分；最小堆用来保存数据流中大的部分，位于排序的数据流中的右半部分。

为了保证两个堆的元素数目之差不能超过1，初始化一个 counter，当 counter 为奇数时，插入左半部分，否则插入右半部分。

奇数情况下，当待插入数字比左边最大的数字小时，将该数字直接插入左边；否则，取出原来左边的最大数字，将这个数字插入右边，同时将待插入数字插入左边。

偶数情况下，当待插入数字比右边最小的数字大时，将该数字直接插入右边；否则，取出原来右边的最小数字，将这个数字插入左边，同时将待插入数字插入右边。

读完数据流之后，取左边的最大数字和右边的最小数字。

当 counter 为奇数， 判断下最大堆和最小堆的容量，哪个大就取哪个的堆顶得到中位数；

当 counter 为偶数，直接取两个堆的堆顶除以二得到中位数。

```javascript
class MedianFinder {
  // static 不能在类的实例上用
  static _minHeap; 
  static _maxHeap;
  static _counter;
  constructor() {
    this._maxHeap = new MaxPriorityQueue(); // 左边
    this._minHeap = new MinPriorityQueue(); // 右边
    this._counter = 0;
  }

  addNum(num) {
    this._counter++;
    if (this._counter % 2 === 1) {
      if (this._minHeap.front() !== null) {
        if (num >= this._minHeap.front().element) {
          const minTop = this._minHeap.dequeue().element;
          this._maxHeap.enqueue(minTop);
          this._minHeap.enqueue(num);
        } else {
          this._maxHeap.enqueue(num);
        }
      } else {
        this._maxHeap.enqueue(num);
      }
    } else {
      if (this._maxHeap.front() !== null) {
        if (num <= this._maxHeap.front().element) {
          const maxTop = this._maxHeap.dequeue().element;
          this._minHeap.enqueue(maxTop);
          this._maxHeap.enqueue(num);
        } else {
          this._minHeap.enqueue(num);
        }
      } else {
        this._minHeap.enqueue(num);
      }
    }
  }

  findMedian() {
    if (this._maxHeap.size() === this._minHeap.size()) {
      return (this._maxHeap.front().element + this._minHeap.front().element) / 2;
    } else {
      return this._maxHeap.size() > this._minHeap.size() ? this._maxHeap.front().element : this._minHeap.front().element;
    }
  }
}

/**
 * Your MedianFinder object will be instantiated and called as such:
 * var obj = new MedianFinder()
 * obj.addNum(num)
 * var param_2 = obj.findMedian()
 */
```

易犯的错误：
1. 最大堆，最小堆初始化反了。

