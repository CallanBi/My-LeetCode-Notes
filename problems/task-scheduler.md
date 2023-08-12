
# 621. Task Scheduler - 任务调度器

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Greedy-贪心-blue.svg">   <img src="https://img.shields.io/badge/Array-数组-blue.svg">   <img src="https://img.shields.io/badge/Hash Table-哈希表-blue.svg">   <img src="https://img.shields.io/badge/Counting-计数-blue.svg">   <img src="https://img.shields.io/badge/Sorting-排序-blue.svg">   <img src="https://img.shields.io/badge/Heap (Priority Queue)-堆（优先队列）-blue.svg">  


## Description - 题目描述

### EN:
<p>Given a characters array <code>tasks</code>, representing the tasks a CPU needs to do, where each letter represents a different task. Tasks could be done in any order. Each task is done in one unit of time. For each unit of time, the CPU could complete either one task or just be idle.</p>

<p>However, there is a non-negative integer&nbsp;<code>n</code> that represents the cooldown period between&nbsp;two <b>same tasks</b>&nbsp;(the same letter in the array), that is that there must be at least <code>n</code> units of time between any two same tasks.</p>

<p>Return <em>the least number of units of times that the CPU will take to finish all the given tasks</em>.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input:</strong> tasks = [&quot;A&quot;,&quot;A&quot;,&quot;A&quot;,&quot;B&quot;,&quot;B&quot;,&quot;B&quot;], n = 2
<strong>Output:</strong> 8
<strong>Explanation:</strong> 
A -&gt; B -&gt; idle -&gt; A -&gt; B -&gt; idle -&gt; A -&gt; B
There is at least 2 units of time between any two same tasks.
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre>
<strong>Input:</strong> tasks = [&quot;A&quot;,&quot;A&quot;,&quot;A&quot;,&quot;B&quot;,&quot;B&quot;,&quot;B&quot;], n = 0
<strong>Output:</strong> 6
<strong>Explanation:</strong> On this case any permutation of size 6 would work since n = 0.
[&quot;A&quot;,&quot;A&quot;,&quot;A&quot;,&quot;B&quot;,&quot;B&quot;,&quot;B&quot;]
[&quot;A&quot;,&quot;B&quot;,&quot;A&quot;,&quot;B&quot;,&quot;A&quot;,&quot;B&quot;]
[&quot;B&quot;,&quot;B&quot;,&quot;B&quot;,&quot;A&quot;,&quot;A&quot;,&quot;A&quot;]
...
And so on.
</pre>

<p><strong class="example">Example 3:</strong></p>

<pre>
<strong>Input:</strong> tasks = [&quot;A&quot;,&quot;A&quot;,&quot;A&quot;,&quot;A&quot;,&quot;A&quot;,&quot;A&quot;,&quot;B&quot;,&quot;C&quot;,&quot;D&quot;,&quot;E&quot;,&quot;F&quot;,&quot;G&quot;], n = 2
<strong>Output:</strong> 16
<strong>Explanation:</strong> 
One possible solution is
A -&gt; B -&gt; C -&gt; A -&gt; D -&gt; E -&gt; A -&gt; F -&gt; G -&gt; A -&gt; idle -&gt; idle -&gt; A -&gt; idle -&gt; idle -&gt; A
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= task.length &lt;= 10<sup>4</sup></code></li>
	<li><code>tasks[i]</code> is upper-case English letter.</li>
	<li>The integer <code>n</code> is in the range <code>[0, 100]</code>.</li>
</ul>


### ZH-CN:
<p>给你一个用字符数组 <code>tasks</code> 表示的 CPU 需要执行的任务列表。其中每个字母表示一种不同种类的任务。任务可以以任意顺序执行，并且每个任务都可以在 1 个单位时间内执行完。在任何一个单位时间，CPU 可以完成一个任务，或者处于待命状态。</p>

<p>然而，两个<strong> 相同种类</strong> 的任务之间必须有长度为整数<strong> </strong><code>n</code><strong> </strong>的冷却时间，因此至少有连续 <code>n</code> 个单位时间内 CPU 在执行不同的任务，或者在待命状态。</p>

<p>你需要计算完成所有任务所需要的<strong> 最短时间</strong> 。</p>

<p> </p>

<p><strong>示例 1：</strong></p>

<pre>
<strong>输入：</strong>tasks = ["A","A","A","B","B","B"], n = 2
<strong>输出：</strong>8
<strong>解释：</strong>A -> B -> (待命) -> A -> B -> (待命) -> A -> B
     在本示例中，两个相同类型任务之间必须间隔长度为 n = 2 的冷却时间，而执行一个任务只需要一个单位时间，所以中间出现了（待命）状态。 </pre>

<p><strong>示例 2：</strong></p>

<pre>
<strong>输入：</strong>tasks = ["A","A","A","B","B","B"], n = 0
<strong>输出：</strong>6
<strong>解释：</strong>在这种情况下，任何大小为 6 的排列都可以满足要求，因为 n = 0
["A","A","A","B","B","B"]
["A","B","A","B","A","B"]
["B","B","B","A","A","A"]
...
诸如此类
</pre>

<p><strong>示例 3：</strong></p>

<pre>
<strong>输入：</strong>tasks = ["A","A","A","A","A","A","B","C","D","E","F","G"], n = 2
<strong>输出：</strong>16
<strong>解释：</strong>一种可能的解决方案是：
     A -> B -> C -> A -> D -> E -> A -> F -> G -> A -> (待命) -> (待命) -> A -> (待命) -> (待命) -> A
</pre>

<p> </p>

<p><strong>提示：</strong></p>

<ul>
	<li><code>1 <= task.length <= 10<sup>4</sup></code></li>
	<li><code>tasks[i]</code> 是大写英文字母</li>
	<li><code>n</code> 的取值范围为 <code>[0, 100]</code></li>
</ul>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/task-scheduler/description/)  -  [LeetCode-CN](https://leetcode.cn/problems/task-scheduler/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| typescript  | 252 ms | 51.6 MB | 2023/08/12 21:35 |

```typescript

function leastInterval(tasks: string[], n: number): number {
  const sortTask = (tasksArr: Array<[string, number, number]>) => {
    tasksArr = tasksArr.sort((a, b) => {
      if (b[2] - a[2] === 0) {
        return a[1] - b[1];
      } else {
        return b[2] - a[2];
      }
    });
  }

  const tasksArr: Array<[string, number, number]> = [];

  for (let i = 0; i < tasks.length; i++) {
    const ele = tasksArr.find(e => e[0] === tasks[i]);
    if (ele) {
      ele[2] += 1;
    } else {
      tasksArr.push([tasks[i], 0, 1]);
    }
  }


  sortTask(tasksArr);

  let time = 0;

  while (tasksArr[0][2] !== 0) {
    if (tasksArr[0][1] !== 0) {
      const i = tasksArr.findIndex(e => e[1] === 0 && e[2] > 0);

      time++;

      if (i === -1) {
        tasksArr.forEach(e => {
          if (e[1] > 0) {
            e[1] -= 1;
          }
        });
      } else {
        tasksArr[i][1] = n;

        tasksArr[i][2] -= 1;

        for (let j = 0; j < tasksArr.length; j++) {
          if (tasksArr[j][1] > 0 && j !== i) {
            tasksArr[j][1] -= 1;
          }
        }

        sortTask(tasksArr);
      }

      continue;
    }

    tasksArr[0][1] = n;

    tasksArr[0][2] -= 1;

    for (let j = 1; j < tasksArr.length; j++) {
      if (tasksArr[j][1] > 0) {
        tasksArr[j][1] -= 1;
      }
    }

    time++;

    sortTask(tasksArr);
  }

  return time;

};

```
## My Notes - 我的笔记


# 贪心

模拟题，自己想出来的贪心思路。

首先，遍历一遍任务列表，构造一个数组，这个数组每个元素类型为`[任务名称, 任务剩余冷却时间, 任务剩余数量]`。

这个数组在每一次任务调度后都会做一次排序，排序规则为首先按照剩余任务次数降序排序，若剩余任务数量相同，则按照剩余冷却时间升序排序。

每一次调度任务时，都需要从这个数组中去取。

首先根据贪心思想，优先取剩余数量最多的任务，故取数组顶端的任务，因为每次排序数组都会将剩余数量最多的任务排在顶端。

如果顶端的剩余数量最多的任务的剩余时间不为0，则表明这类任务还在冷却中，则根据贪心思想，优先取剩余冷却时间为0且数量最多的任务。故可以顺着数组顶端往下寻找，找到第一个剩余冷却时间为0且剩余数量>0的任务。

上述两种情况如果找到了，就开始执行：

1. 将当前类的任务的剩余冷却时间置为`n`，代表执行序列加入了当前任务，当前类任务重新冷却；
2. 将当前类的任务剩余数量 -1，代表代表执行序列加入了当前任务；
3. 对于每一个其他非当前类任务，剩余冷却时间 -1（需要判断冷却时间是否大于0，若等于 0 则不用减），代表时间推移，剩余冷却时间减少；
4. 对时间+1；

如果上述两种情况都不存在，说明所有任务都在冷却时间中，则：

1. 对所有任务的剩余冷却时间-1；
2. 对时间+1；

最后返回时间即可。

```typescript
function leastInterval(tasks: string[], n: number): number {
  const sortTask = (tasksArr: Array<[string, number, number]>) => {
    tasksArr = tasksArr.sort((a, b) => {
      if (b[2] - a[2] === 0) {
        return a[1] - b[1];
      } else {
        return b[2] - a[2];
      }
    });
  }

  const tasksArr: Array<[string, number, number]> = [];

  for (let i = 0; i < tasks.length; i++) {
    const ele = tasksArr.find(e => e[0] === tasks[i]);
    if (ele) {
      ele[2] += 1;
    } else {
      tasksArr.push([tasks[i], 0, 1]);
    }
  }


  sortTask(tasksArr);

  let time = 0;

  while (tasksArr[0][2] !== 0) {
    if (tasksArr[0][1] !== 0) {
      const i = tasksArr.findIndex(e => e[1] === 0 && e[2] > 0);

      time++;

      if (i === -1) {
        tasksArr.forEach(e => {
          if (e[1] > 0) {
            e[1] -= 1;
          }
        });
      } else {
        tasksArr[i][1] = n;

        tasksArr[i][2] -= 1;

        for (let j = 0; j < tasksArr.length; j++) {
          if (tasksArr[j][1] > 0 && j !== i) {
            tasksArr[j][1] -= 1;
          }
        }

        sortTask(tasksArr);
      }

      continue;
    }

    tasksArr[0][1] = n;

    tasksArr[0][2] -= 1;

    for (let j = 1; j < tasksArr.length; j++) {
      if (tasksArr[j][1] > 0) {
        tasksArr[j][1] -= 1;
      }
    }

    time++;

    sortTask(tasksArr);
  }

  return time;

};
```

