
# 剑指 Offer 59 - I. 滑动窗口的最大值 LCOF - 滑动窗口的最大值

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Queue-队列-blue.svg">   <img src="https://img.shields.io/badge/Sliding Window-滑动窗口-blue.svg">   <img src="https://img.shields.io/badge/Monotonic Queue-单调队列-blue.svg">   <img src="https://img.shields.io/badge/Heap (Priority Queue)-堆（优先队列）-blue.svg">  


## Description - 题目描述

### EN:
<p>English description is not available for the problem. Please switch to Chinese.</p>


### ZH-CN:
<p>给定一个数组 <code>nums</code> 和滑动窗口的大小 <code>k</code>，请找出所有滑动窗口里的最大值。</p>

<p><strong>示例:</strong></p>

<pre>
<strong>输入:</strong> <em>nums</em> = <code>[1,3,-1,-3,5,3,6,7]</code>, 和 <em>k</em> = 3
<strong>输出: </strong><code>[3,3,5,5,6,7] 
<strong>解释: 
</strong></code>
  滑动窗口的位置                最大值
---------------               -----
[1  3  -1] -3  5  3  6  7       3
 1 [3  -1  -3] 5  3  6  7       3
 1  3 [-1  -3  5] 3  6  7       5
 1  3  -1 [-3  5  3] 6  7       5
 1  3  -1  -3 [5  3  6] 7       6
 1  3  -1  -3  5 [3  6  7]      7</pre>

<p>&nbsp;</p>

<p><strong>提示：</strong></p>

<p>你可以假设 <em>k </em>总是有效的，在输入数组&nbsp;<strong>不为空&nbsp;</strong>的情况下，<code>1 ≤ k ≤&nbsp;nums.length</code>。</p>

<p>注意：本题与主站 239 题相同：<a href="https://leetcode-cn.com/problems/sliding-window-maximum/">https://leetcode-cn.com/problems/sliding-window-maximum/</a></p>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/hua-dong-chuang-kou-de-zui-da-zhi-lcof/description/)  -  [LeetCode-CN](https://leetcode.cn/problems/hua-dong-chuang-kou-de-zui-da-zhi-lcof/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| typescript  | 92 ms | 48.1 MB | 2022/04/23 18:40 |

```typescript

function maxSlidingWindow(nums: number[], k: number): number[] {
  if (nums.length == 0 || k === 0) {
    return [];
  }
  
  if (k === 1) {
    return nums;
  }

  const monotoneQueue: number[] = [], res: number[] = [];

  for (let i = 0; i < k; i++) {
    while (monotoneQueue[monotoneQueue.length - 1] !== undefined && monotoneQueue[monotoneQueue.length - 1] < nums[i]) {
      monotoneQueue.pop();
    }
    monotoneQueue.push(nums[i]);
  }

  if (nums[0] === monotoneQueue[0]) {
    const top = monotoneQueue.shift();
    res.push(top);
  } else {
    res.push(monotoneQueue[0]);
  }

  for (let i = k; i < nums.length; i++) {
    while (monotoneQueue[monotoneQueue.length - 1] !== undefined && monotoneQueue[monotoneQueue.length - 1] < nums[i]) {
      monotoneQueue.pop();
    }
    monotoneQueue.push(nums[i]);

    if (nums[i - k + 1] === monotoneQueue[0]) {
      const top = monotoneQueue.shift();
      res.push(top);
    } else {
      res.push(monotoneQueue[0]);
    }
  }

  return res;
};

```
## My Notes - 我的笔记


# 单调队列

在滑动窗口有关问题中，滑动窗口可以看做一个**队列**。

剑指 offer 的方法：单调队列。

维护一个只存放可能成为滑动窗口最大值的单调**双端**队列。

这个队列需要是单调不增的。如果滑动窗口滑动时，只需要插入序列的下一个数字。

如果窗口里有数字比它小，就 pop() 这些数字再入队列。

如果没有则直接入队列。

队列的长度最多为 k。如果队列头部数字已经被滑出，需要对头部的数字出队列。

```typescript
function maxSlidingWindow(nums: number[], k: number): number[] {
  if (nums.length == 0 || k === 0) {
    return [];
  }
  
  if (k === 1) {
    return nums;
  }

  const monotoneQueue: number[] = [], res: number[] = [];

  for (let i = 0; i < k; i++) {
	// 窗口里有数字比它小，就 pop() 这些数字再入队列
    while (monotoneQueue[monotoneQueue.length - 1] !== undefined && monotoneQueue[monotoneQueue.length - 1] < nums[i]) {
      monotoneQueue.pop();
    }
	// 否则直接入队列
    monotoneQueue.push(nums[i]);
  }

  // 如果队列头部数字已经被滑出，需要对头部的数字出队列
  if (nums[0] === monotoneQueue[0]) {
    const top = monotoneQueue.shift();
    res.push(top);
  } else {
    res.push(monotoneQueue[0]);
  }

  for (let i = k; i < nums.length; i++) {
	// 窗口里有数字比它小，就 pop() 这些数字再入队列
    while (monotoneQueue[monotoneQueue.length - 1] !== undefined && monotoneQueue[monotoneQueue.length - 1] < nums[i]) {
      monotoneQueue.pop();
    }
	// 否则直接入队列
    monotoneQueue.push(nums[i]);

    // 如果队列头部数字已经被滑出，需要对头部的数字出队列
    if (nums[i - k + 1] === monotoneQueue[0]) {
      const top = monotoneQueue.shift();
      res.push(top);
    } else {
      res.push(monotoneQueue[0]);
    }
  }

  return res;
};
```

时间复杂度： $O(n)$

空间复杂度：$O(k)$

# 优先队列

维护一个最大堆，则堆顶就是最大值。

最开始，我们把第一个滑动窗口的元素全部都喂给最大堆，然后堆顶便是最大值。

当窗口向右滑动时，我们让滑动窗口中新的元素入堆，此时再拿一下堆顶。

但这个堆顶有可能不在滑动窗口中。如果它不在窗口的话，就移除堆顶。直到新的堆顶在滑动窗口中为止。

此时，这个堆顶就是滑动窗口的最大值。

如何判断堆顶在不在滑动窗口中？我们可以用二元组`[key, value]`（或一个对象`{ key: number; value: number }`）存储 `nums` 的值和索引，每次拿到堆顶时，将这个索引与滑动窗口范围比较即可。



时间复杂度： $O(n \log n)$

空间复杂度：$O(n)$


