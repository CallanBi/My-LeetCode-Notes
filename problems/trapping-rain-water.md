
# 42. Trapping Rain Water - 接雨水

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Stack-栈-blue.svg">   <img src="https://img.shields.io/badge/Array-数组-blue.svg">   <img src="https://img.shields.io/badge/Two Pointers-双指针-blue.svg">   <img src="https://img.shields.io/badge/Dynamic Programming-动态规划-blue.svg">   <img src="https://img.shields.io/badge/Monotonic Stack-单调栈-blue.svg">  


## Description - 题目描述

### EN:
<p>Given <code>n</code> non-negative integers representing an elevation map where the width of each bar is <code>1</code>, compute how much water it can trap after raining.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>
<img src="https://assets.leetcode.com/uploads/2018/10/22/rainwatertrap.png" style="width: 412px; height: 161px;" />
<pre>
<strong>Input:</strong> height = [0,1,0,2,1,0,1,3,2,1,2,1]
<strong>Output:</strong> 6
<strong>Explanation:</strong> The above elevation map (black section) is represented by array [0,1,0,2,1,0,1,3,2,1,2,1]. In this case, 6 units of rain water (blue section) are being trapped.
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre>
<strong>Input:</strong> height = [4,2,0,3,2,5]
<strong>Output:</strong> 9
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>n == height.length</code></li>
	<li><code>1 &lt;= n &lt;= 2 * 10<sup>4</sup></code></li>
	<li><code>0 &lt;= height[i] &lt;= 10<sup>5</sup></code></li>
</ul>


### ZH-CN:
<p>给定&nbsp;<code>n</code> 个非负整数表示每个宽度为 <code>1</code> 的柱子的高度图，计算按此排列的柱子，下雨之后能接多少雨水。</p>

<p>&nbsp;</p>

<p><strong>示例 1：</strong></p>

<p><img src="https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2018/10/22/rainwatertrap.png" style="height: 161px; width: 412px;" /></p>

<pre>
<strong>输入：</strong>height = [0,1,0,2,1,0,1,3,2,1,2,1]
<strong>输出：</strong>6
<strong>解释：</strong>上面是由数组 [0,1,0,2,1,0,1,3,2,1,2,1] 表示的高度图，在这种情况下，可以接 6 个单位的雨水（蓝色部分表示雨水）。 
</pre>

<p><strong>示例 2：</strong></p>

<pre>
<strong>输入：</strong>height = [4,2,0,3,2,5]
<strong>输出：</strong>9
</pre>

<p>&nbsp;</p>

<p><strong>提示：</strong></p>

<ul>
	<li><code>n == height.length</code></li>
	<li><code>1 &lt;= n &lt;= 2 * 10<sup>4</sup></code></li>
	<li><code>0 &lt;= height[i] &lt;= 10<sup>5</sup></code></li>
</ul>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/trapping-rain-water/description/)  -  [LeetCode-CN](https://leetcode.cn/problems/trapping-rain-water/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| typescript  | 84 ms | 43.9 MB | 2022/04/10 19:31 |

```typescript

/** two pointers */
function trap(height: number[]): number {
   if (height.length < 3) {
    return 0;
  }

  let ans = 0;

  let i = 0, j = height.length - 1;

  let curLeftMax = 0, curRightMax = 0;

  while (i < j) {
    curLeftMax = Math.max(height[i], curLeftMax);
    curRightMax = Math.max(height[j], curRightMax);
    if (curLeftMax < curRightMax) {
      ans += curLeftMax - height[i];
      i++;
    } else {
       ans += curRightMax - height[j];
      j--;
    }
  }

  return ans;
};

```
## My Notes - 我的笔记


三种方法：动态规划、单调栈和双指针。

# 动态规划

思路：遍历两遍数组，分别得到 leftMax 和 rightMax 两个递推的动态规划表，再遍历这两个表取最小的，减去当前柱子的高度即可。

```typescript
 /** dp */
function trap(height: number[]): number {
  if (height.length < 3) {
    return 0;
  }

  let ans = 0;

  const leftMax = [];
  const rightMax = [];

  for (let i = 0; i < height.length; i++) {
    leftMax[i] = Math.max(height[i], leftMax[i-1] ?? 0);
  }

  for (let j = height.length - 1; j >= 0; j--) {
    rightMax[j] = Math.max(height[j], rightMax[j+1] ?? 0);
  }

  for (let k = 0; k < height.length; k++) {
    ans += Math.min(leftMax[k], rightMax[k]) - height[k];
  }

  return ans;
};
```

时间复杂度：$O(n)$，空间复杂度：$O(n)$

# 单调栈

对于每一个 `height[i]`，如果它比 `height[i-1]`小，那么它便是有可能存储雨水的地方。如果后面遇到一个比 `height[i]` 高的柱子，就可以存储雨水。

基于有可能存储雨水的地方需要比之前的柱子小这一特性，可以维护一个单调不增栈。入栈元素是`height` 的下标。 这样遇到 `height[i]` 比栈顶大的情况时，都要出栈并计算 **刚刚出栈的元素所在的地方** 与 **出栈后的栈顶** 和  **`height[i]`** 组成的区域围起来的地方能存储多少雨水，直到没有元素可以出栈为止，这样就可以保证栈是单调的。

伪代码可以这样表示：

```markdown
    遍历 height，对于每一个 height[i]:
      当 栈不为空 且 height[i] 比 栈顶 大：
        将当前栈顶出栈；
        计算当前位置到 **当前** 栈顶索引的宽度；
        取当前高度与栈顶的最小值，减去 **刚刚出栈的元素** 索引所在的柱子的高度，乘上计算出来的宽度，累加到 res 上；
      将当前 height[i] 入栈
```

代码：

```typescript
/** monotonic stack */
function trap(height: number[]): number {
  if (height.length <= 2) {
    return 0;
  }

  const monotonicStack = [0];

  let ans = 0;

  for (let i = 1; i < height.length; i++) {
    while (monotonicStack.length > 0 && height[monotonicStack[monotonicStack.length-1]] < height[i]) {
      const curIdx = monotonicStack.pop();
      const cur = height[curIdx];
      const left = height[monotonicStack[monotonicStack.length-1]] || 0;
      const width = i - monotonicStack[monotonicStack.length-1] - 1 || 0;
      const right = height[i];
      const area = (Math.min(left, right) - cur) * width;
      ans += area;
    }
    monotonicStack.push(i);
  }
  return ans;
};
```

时间复杂度： $O(n)$， 空间复杂度： $O(n)$

# 双指针

在动态规划方法中，下标 i 处能接的雨水量由 `leftMax}[i]` 和 `rightMax[i]`中的最小值决定。由于数组`leftMax` 是从左往右计算，数组 `rightMax` 是从右往左计算，因此可以使用双指针和两个变量代替两个数组。

为什么空间复杂度可以优化，就是因为这个动态规划中 `dp[i]` 的状态是仅由 `dp[i-1]` 决定的。

但这样的话，不用双指针还是需要遍历三遍。那怎么优化成双指针只需要遍历一遍呢？

双指针移动的条件一定是当指针所在位置较小时才能移动。这样才能保证取的是这个地方两边高度最小。这样就可以遍历一遍了。

代码：

```typescript
/** two pointers */
function trap(height: number[]): number {
   if (height.length < 3) {
    return 0;
  }

  let ans = 0;

  let i = 0, j = height.length - 1;

  let curLeftMax = 0, curRightMax = 0;

  while (i < j) {
    curLeftMax = Math.max(height[i], curLeftMax);
    curRightMax = Math.max(height[j], curRightMax);
    if (curLeftMax < curRightMax) {
      ans += curLeftMax - height[i];
      i++;
    } else {
       ans += curRightMax - height[j];
      j--;
    }
  }

  return ans;
};
```

时间复杂度：$O(1)$，空间复杂度：$O(1)$


