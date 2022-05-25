
# 剑指 Offer 49. 丑数 LCOF - 丑数

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Hash Table-哈希表-blue.svg">   <img src="https://img.shields.io/badge/Math-数学-blue.svg">   <img src="https://img.shields.io/badge/Dynamic Programming-动态规划-blue.svg">   <img src="https://img.shields.io/badge/Heap (Priority Queue)-堆（优先队列）-blue.svg">  


## Description - 题目描述

### EN:
English description is not available for the problem. Please switch to Chinese.

### ZH-CN:
<p>我们把只包含质因子 2、3 和 5 的数称作丑数（Ugly Number）。求按从小到大的顺序的第 n 个丑数。</p>

<p>&nbsp;</p>

<p><strong>示例:</strong></p>

<pre><strong>输入:</strong> n = 10
<strong>输出:</strong> 12
<strong>解释: </strong><code>1, 2, 3, 4, 5, 6, 8, 9, 10, 12</code> 是前 10 个丑数。</pre>

<p><strong>说明:&nbsp;</strong>&nbsp;</p>

<ol>
	<li><code>1</code>&nbsp;是丑数。</li>
	<li><code>n</code>&nbsp;<strong>不超过</strong>1690。</li>
</ol>

<p>注意：本题与主站 264 题相同：<a href="https://leetcode-cn.com/problems/ugly-number-ii/">https://leetcode-cn.com/problems/ugly-number-ii/</a></p>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/chou-shu-lcof/description/)  -  [LeetCode-CN](https://leetcode-cn.com/problems/chou-shu-lcof/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| javascript  | 176 ms | 46.1 MB | 2021/12/20 16:32 |

```javascript

/**
 * @param {number} n
 * @return {number}
 */
function nthUglyNumber(n) {
  if (n === 1) {
    return 1;
  }
  const uglyGroup = new Set();
  uglyGroup.add(1);
  const heap = new MinPriorityQueue();
  heap.enqueue(1);
  const factor = [2, 3, 5];
  for (let i = 1; i < n; i++) {
    const top = heap.dequeue().element;
    for (let f of factor) {
      const newNum = f * top;
      if (!uglyGroup.has(newNum)) {
        heap.enqueue(newNum);
        uglyGroup.add(newNum);
      }
    }
  }
  return heap.dequeue().element;
};

```
## My Notes - 我的笔记


# 最直观的思路，会超出时间限制

```typescript
function nthUglyNumber(n: number): number {
  if (n === 1) {
    return 1;
  }
  let counter = 1, num = 1;
  while (counter < n) {
    num++;
    if (isUglyNumber(num)) {
      counter++;
    }
  }
  return num;
};

function isUglyNumber(num: number): boolean {
  while (num % 2 === 0) {
    num /= 2;
  }
  while (num % 3 === 0) {
    num /= 3;
  }
  while (num % 5 === 0) {
    num /= 5;
  }
  return num === 1;
}
```

时间复杂度： $O(nlogn)$

空间复杂度: $O(1)$

# 最小堆

思路：令初始乘因子为{2, 3, 5}，将1加入丑数容器即最小堆。对于每一个容器中的数，2x, 3x, 5x 一定也是丑数。所以只需要把容器中最小的数x取出来， 再将2x，3x，5x 加入进去即可。

可以用 set  去重已取出来的数，保证插入的数不在已取出来的数中。

```javascript
/**
 * @param {number} n
 * @return {number}
 */
function nthUglyNumber(n) {
  if (n === 1) {
    return 1;
  }
  const uglyGroup = new Set();
  uglyGroup.add(1);
  const heap = new MinPriorityQueue();
  heap.enqueue(1);
  const factor = [2, 3, 5];
  for (let i = 1; i < n; i++) {
    const top = heap.dequeue().element;
    for (let f of factor) {
      const newNum = f * top;
      if (!uglyGroup.has(newNum)) {
        heap.enqueue(newNum);
        uglyGroup.add(newNum);
      }
    }
  }
  return heap.dequeue().element;
};
```

时间复杂度： $O(nlogn)$

空间复杂度: $O(n)$

# 动态规划（三指针）

思路：模拟一下手写丑数的过程就能找到规律。题解参考[这里](https://leetcode-cn.com/problems/ugly-number-ii/solution/bao-li-you-xian-dui-lie-xiao-ding-dui-dong-tai-gui/)。

设 $p2, p3, p5$ 代表 `dp` 中某个元素的索引，对应元素分别乘上二倍、三倍、五倍取最小值得到第 `n` 个丑数。 初始时令这三个指针位置相同，$  p2 = p3 = p5 = 1 $。

状态转移方程： $dp[i] = min\{2 \times dp[p2], 3 \times dp[p3], 5 \times dp[p5]\}$

代码：

```typescript
function nthUglyNumber(n: number): number {
  const dp: number[] = [0, 1];

  if (n === 1) {
    return dp[n];
  }

  let p2 = 1, p3 = 1, p5 = 1;

  for (let i = 2; i <= n; i++) {
    dp[i] = Math.min(2 * dp[p2], 3 * dp[p3], 5 * dp[p5]);

    if (dp[i] === 2 * dp[p2]) {
      ++p2;
    }
    if (dp[i] === 3 * dp[p3]) {
      ++p3;
    }
    if (dp[i] === 5 * dp[p5]) {
      ++p5;
    }
  }

  return dp[n];
};
```

时间复杂度： $O(n)$

空间复杂度: $O(n)$



