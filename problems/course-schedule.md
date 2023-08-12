
# 207. Course Schedule - 课程表

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Depth First Search-深度优先搜索-blue.svg">   <img src="https://img.shields.io/badge/Breadth First Search-广度优先搜索-blue.svg">   <img src="https://img.shields.io/badge/Graph-图-blue.svg">   <img src="https://img.shields.io/badge/Topological Sort-拓扑排序-blue.svg">  


## Description - 题目描述

### EN:
<p>There are a total of <code>numCourses</code> courses you have to take, labeled from <code>0</code> to <code>numCourses - 1</code>. You are given an array <code>prerequisites</code> where <code>prerequisites[i] = [a<sub>i</sub>, b<sub>i</sub>]</code> indicates that you <strong>must</strong> take course <code>b<sub>i</sub></code> first if you want to take course <code>a<sub>i</sub></code>.</p>

<ul>
	<li>For example, the pair <code>[0, 1]</code>, indicates that to take course <code>0</code> you have to first take course <code>1</code>.</li>
</ul>

<p>Return <code>true</code> if you can finish all courses. Otherwise, return <code>false</code>.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input:</strong> numCourses = 2, prerequisites = [[1,0]]
<strong>Output:</strong> true
<strong>Explanation:</strong> There are a total of 2 courses to take. 
To take course 1 you should have finished course 0. So it is possible.
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre>
<strong>Input:</strong> numCourses = 2, prerequisites = [[1,0],[0,1]]
<strong>Output:</strong> false
<strong>Explanation:</strong> There are a total of 2 courses to take. 
To take course 1 you should have finished course 0, and to take course 0 you should also have finished course 1. So it is impossible.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= numCourses &lt;= 2000</code></li>
	<li><code>0 &lt;= prerequisites.length &lt;= 5000</code></li>
	<li><code>prerequisites[i].length == 2</code></li>
	<li><code>0 &lt;= a<sub>i</sub>, b<sub>i</sub> &lt; numCourses</code></li>
	<li>All the pairs prerequisites[i] are <strong>unique</strong>.</li>
</ul>


### ZH-CN:
<p>你这个学期必须选修 <code>numCourses</code> 门课程，记为&nbsp;<code>0</code>&nbsp;到&nbsp;<code>numCourses - 1</code> 。</p>

<p>在选修某些课程之前需要一些先修课程。 先修课程按数组&nbsp;<code>prerequisites</code> 给出，其中&nbsp;<code>prerequisites[i] = [a<sub>i</sub>, b<sub>i</sub>]</code> ，表示如果要学习课程&nbsp;<code>a<sub>i</sub></code> 则 <strong>必须</strong> 先学习课程&nbsp; <code>b<sub>i</sub></code><sub> </sub>。</p>

<ul>
	<li>例如，先修课程对&nbsp;<code>[0, 1]</code> 表示：想要学习课程 <code>0</code> ，你需要先完成课程 <code>1</code> 。</li>
</ul>

<p>请你判断是否可能完成所有课程的学习？如果可以，返回 <code>true</code> ；否则，返回 <code>false</code> 。</p>

<p>&nbsp;</p>

<p><strong>示例 1：</strong></p>

<pre>
<strong>输入：</strong>numCourses = 2, prerequisites = [[1,0]]
<strong>输出：</strong>true
<strong>解释：</strong>总共有 2 门课程。学习课程 1 之前，你需要完成课程 0 。这是可能的。</pre>

<p><strong>示例 2：</strong></p>

<pre>
<strong>输入：</strong>numCourses = 2, prerequisites = [[1,0],[0,1]]
<strong>输出：</strong>false
<strong>解释：</strong>总共有 2 门课程。学习课程 1 之前，你需要先完成​课程 0 ；并且学习课程 0 之前，你还应先完成课程 1 。这是不可能的。</pre>

<p>&nbsp;</p>

<p><strong>提示：</strong></p>

<ul>
	<li><code>1 &lt;= numCourses &lt;= 2000</code></li>
	<li><code>0 &lt;= prerequisites.length &lt;= 5000</code></li>
	<li><code>prerequisites[i].length == 2</code></li>
	<li><code>0 &lt;= a<sub>i</sub>, b<sub>i</sub> &lt; numCourses</code></li>
	<li><code>prerequisites[i]</code> 中的所有课程对 <strong>互不相同</strong></li>
</ul>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/course-schedule/description/)  -  [LeetCode-CN](https://leetcode.cn/problems/course-schedule/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| typescript  | 80 ms | 45.9 MB | 2023/03/18 20:14 |

```typescript

function canFinish(numCourses: number, prerequisites: number[][]): boolean {
  if (prerequisites.length === 0 || numCourses === 1) {
    return true;
  }

  let hasCircle = false;

  const map = new Map<number, {
    /** 0: unfinished, 1: searching, 2: finished */
    status: 0 | 1 | 2;
    nodes: number[];
  }>();

  for (let i = 0; i < prerequisites.length; i++) {
    const cur = prerequisites[i][0];
    const iNode = map.get(prerequisites[i][0]);
    if (!iNode) {
      map.set(cur, {
        status: 0,
        nodes: [prerequisites[i][1]],
      })
    } else {
      iNode.nodes.push(prerequisites[i][1]);
    }
  }

  const dfs = (node: number) => {
    const obj = map.get(node);
    if (!obj) {
      return false;
    }
    if (obj.status === 1) {
      hasCircle = true;
      return true;
    }
    if (obj.status === 2) {
      return false;
    }
    obj.status = 1;
    for (let i = 0; i < obj.nodes.length; i++) {
      const childHasCircle = dfs(obj.nodes[i]);
      if (childHasCircle) {
        return true;
      }
    }
    obj.status = 2;
    return false;
  }


  // check isDag
  for (const k of map.keys()) {
    hasCircle = dfs(k);
    if (hasCircle) {
      return false;
    }
  }


  return !hasCircle;
};

```
## My Notes - 我的笔记


按照官方题解，先构造图，再dfs 即可。注意及时 return 剪枝。
```typescript
function canFinish(numCourses: number, prerequisites: number[][]): boolean {
  if (prerequisites.length === 0 || numCourses === 1) {
    return true;
  }

  let hasCircle = false;

  const map = new Map<number, {
    /** 0: unfinished, 1: searching, 2: finished */
    status: 0 | 1 | 2;
    nodes: number[];
  }>();

  for (let i = 0; i < prerequisites.length; i++) {
    const cur = prerequisites[i][0];
    const iNode = map.get(prerequisites[i][0]);
    if (!iNode) {
      map.set(cur, {
        status: 0,
        nodes: [prerequisites[i][1]],
      })
    } else {
      iNode.nodes.push(prerequisites[i][1]);
    }
  }

  const dfs = (node: number) => {
    const obj = map.get(node);
    if (!obj) {
      return false;
    }
    if (obj.status === 1) {
      hasCircle = true;
      return true;
    }
    if (obj.status === 2) {
      return false;
    }
    obj.status = 1;
    for (let i = 0; i < obj.nodes.length; i++) {
      const childHasCircle = dfs(obj.nodes[i]);
      if (childHasCircle) {
        return true;
      }
    }
    obj.status = 2;
    return false;
  }


  // check isDag
  for (const k of map.keys()) {
    hasCircle = dfs(k);
    if (hasCircle) {
      return false;
    }
  }

  return !hasCircle;
};
```

