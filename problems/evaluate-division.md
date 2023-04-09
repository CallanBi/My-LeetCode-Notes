
# 399. Evaluate Division - 除法求值

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Depth First Search-深度优先搜索-blue.svg">   <img src="https://img.shields.io/badge/Breadth First Search-广度优先搜索-blue.svg">   <img src="https://img.shields.io/badge/Union Find-并查集-blue.svg">   <img src="https://img.shields.io/badge/Graph-图-blue.svg">   <img src="https://img.shields.io/badge/Array-数组-blue.svg">   <img src="https://img.shields.io/badge/Shortest Path-最短路-blue.svg">  


## Description - 题目描述

### EN:
<p>You are given an array of variable pairs <code>equations</code> and an array of real numbers <code>values</code>, where <code>equations[i] = [A<sub>i</sub>, B<sub>i</sub>]</code> and <code>values[i]</code> represent the equation <code>A<sub>i</sub> / B<sub>i</sub> = values[i]</code>. Each <code>A<sub>i</sub></code> or <code>B<sub>i</sub></code> is a string that represents a single variable.</p>

<p>You are also given some <code>queries</code>, where <code>queries[j] = [C<sub>j</sub>, D<sub>j</sub>]</code> represents the <code>j<sup>th</sup></code> query where you must find the answer for <code>C<sub>j</sub> / D<sub>j</sub> = ?</code>.</p>

<p>Return <em>the answers to all queries</em>. If a single answer cannot be determined, return <code>-1.0</code>.</p>

<p><strong>Note:</strong> The input is always valid. You may assume that evaluating the queries will not result in division by zero and that there is no contradiction.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input:</strong> equations = [[&quot;a&quot;,&quot;b&quot;],[&quot;b&quot;,&quot;c&quot;]], values = [2.0,3.0], queries = [[&quot;a&quot;,&quot;c&quot;],[&quot;b&quot;,&quot;a&quot;],[&quot;a&quot;,&quot;e&quot;],[&quot;a&quot;,&quot;a&quot;],[&quot;x&quot;,&quot;x&quot;]]
<strong>Output:</strong> [6.00000,0.50000,-1.00000,1.00000,-1.00000]
<strong>Explanation:</strong> 
Given: <em>a / b = 2.0</em>, <em>b / c = 3.0</em>
queries are: <em>a / c = ?</em>, <em>b / a = ?</em>, <em>a / e = ?</em>, <em>a / a = ?</em>, <em>x / x = ?</em>
return: [6.0, 0.5, -1.0, 1.0, -1.0 ]
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre>
<strong>Input:</strong> equations = [[&quot;a&quot;,&quot;b&quot;],[&quot;b&quot;,&quot;c&quot;],[&quot;bc&quot;,&quot;cd&quot;]], values = [1.5,2.5,5.0], queries = [[&quot;a&quot;,&quot;c&quot;],[&quot;c&quot;,&quot;b&quot;],[&quot;bc&quot;,&quot;cd&quot;],[&quot;cd&quot;,&quot;bc&quot;]]
<strong>Output:</strong> [3.75000,0.40000,5.00000,0.20000]
</pre>

<p><strong class="example">Example 3:</strong></p>

<pre>
<strong>Input:</strong> equations = [[&quot;a&quot;,&quot;b&quot;]], values = [0.5], queries = [[&quot;a&quot;,&quot;b&quot;],[&quot;b&quot;,&quot;a&quot;],[&quot;a&quot;,&quot;c&quot;],[&quot;x&quot;,&quot;y&quot;]]
<strong>Output:</strong> [0.50000,2.00000,-1.00000,-1.00000]
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= equations.length &lt;= 20</code></li>
	<li><code>equations[i].length == 2</code></li>
	<li><code>1 &lt;= A<sub>i</sub>.length, B<sub>i</sub>.length &lt;= 5</code></li>
	<li><code>values.length == equations.length</code></li>
	<li><code>0.0 &lt; values[i] &lt;= 20.0</code></li>
	<li><code>1 &lt;= queries.length &lt;= 20</code></li>
	<li><code>queries[i].length == 2</code></li>
	<li><code>1 &lt;= C<sub>j</sub>.length, D<sub>j</sub>.length &lt;= 5</code></li>
	<li><code>A<sub>i</sub>, B<sub>i</sub>, C<sub>j</sub>, D<sub>j</sub></code> consist of lower case English letters and digits.</li>
</ul>


### ZH-CN:
<p>给你一个变量对数组 <code>equations</code> 和一个实数值数组 <code>values</code> 作为已知条件，其中 <code>equations[i] = [A<sub>i</sub>, B<sub>i</sub>]</code> 和 <code>values[i]</code> 共同表示等式 <code>A<sub>i</sub> / B<sub>i</sub> = values[i]</code> 。每个 <code>A<sub>i</sub></code> 或 <code>B<sub>i</sub></code> 是一个表示单个变量的字符串。</p>

<p>另有一些以数组 <code>queries</code> 表示的问题，其中 <code>queries[j] = [C<sub>j</sub>, D<sub>j</sub>]</code> 表示第 <code>j</code> 个问题，请你根据已知条件找出 <code>C<sub>j</sub> / D<sub>j</sub> = ?</code> 的结果作为答案。</p>

<p>返回 <strong>所有问题的答案</strong> 。如果存在某个无法确定的答案，则用 <code>-1.0</code> 替代这个答案。如果问题中出现了给定的已知条件中没有出现的字符串，也需要用 <code>-1.0</code> 替代这个答案。</p>

<p><strong>注意：</strong>输入总是有效的。你可以假设除法运算中不会出现除数为 0 的情况，且不存在任何矛盾的结果。</p>

<p> </p>

<p><strong>示例 1：</strong></p>

<pre>
<strong>输入：</strong>equations = [["a","b"],["b","c"]], values = [2.0,3.0], queries = [["a","c"],["b","a"],["a","e"],["a","a"],["x","x"]]
<strong>输出：</strong>[6.00000,0.50000,-1.00000,1.00000,-1.00000]
<strong>解释：</strong>
条件：<em>a / b = 2.0</em>, <em>b / c = 3.0</em>
问题：<em>a / c = ?</em>, <em>b / a = ?</em>, <em>a / e = ?</em>, <em>a / a = ?</em>, <em>x / x = ?</em>
结果：[6.0, 0.5, -1.0, 1.0, -1.0 ]
</pre>

<p><strong>示例 2：</strong></p>

<pre>
<strong>输入：</strong>equations = [["a","b"],["b","c"],["bc","cd"]], values = [1.5,2.5,5.0], queries = [["a","c"],["c","b"],["bc","cd"],["cd","bc"]]
<strong>输出：</strong>[3.75000,0.40000,5.00000,0.20000]
</pre>

<p><strong>示例 3：</strong></p>

<pre>
<strong>输入：</strong>equations = [["a","b"]], values = [0.5], queries = [["a","b"],["b","a"],["a","c"],["x","y"]]
<strong>输出：</strong>[0.50000,2.00000,-1.00000,-1.00000]
</pre>

<p> </p>

<p><strong>提示：</strong></p>

<ul>
	<li><code>1 <= equations.length <= 20</code></li>
	<li><code>equations[i].length == 2</code></li>
	<li><code>1 <= A<sub>i</sub>.length, B<sub>i</sub>.length <= 5</code></li>
	<li><code>values.length == equations.length</code></li>
	<li><code>0.0 < values[i] <= 20.0</code></li>
	<li><code>1 <= queries.length <= 20</code></li>
	<li><code>queries[i].length == 2</code></li>
	<li><code>1 <= C<sub>j</sub>.length, D<sub>j</sub>.length <= 5</code></li>
	<li><code>A<sub>i</sub>, B<sub>i</sub>, C<sub>j</sub>, D<sub>j</sub></code> 由小写英文字母与数字组成</li>
</ul>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/evaluate-division/description/)  -  [LeetCode-CN](https://leetcode.cn/problems/evaluate-division/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| typescript  | 68 ms | 42.6 MB | 2023/04/09 21:20 |

```typescript

function calcEquation(equations: string[][], values: number[], queries: string[][]): number[] {
  // construst the graph
  const graph: Map<string, [string, number][]> = new Map();

  for (let i = 0; i < equations.length; i++) {
    const zero = graph.get(equations[i][0])
    if (!zero) {
      graph.set(equations[i][0], [[equations[i][1], values[i]]]);
    } else {
      zero.push([equations[i][1], values[i]])
    }

    const one = graph.get(equations[i][1])
    if (!one) {
      graph.set(equations[i][1], [[equations[i][0], 1 / values[i]]]);
    } else {
      one.push([equations[i][0], 1 / values[i]])
    }
  }


  const dfs = (node: string, target: string, visited: Set<string>, value: number) => {
    if (!graph.get(node)) {
      return -1;
    }

    if (node === target) {
      return value;
    }

    const edges = graph.get(node);

    visited.add(node);

    for (let i = 0; i < edges.length; i++) {
      if (visited.has(edges[i][0])) {
        continue;
      }
      const val = dfs(edges[i][0], target, visited, edges[i][1] * value);
      if (val !== -1) {
        return val;
      }
    }

    return -1;
  }

  const res = new Array(queries.length).fill(-1);

  for (let i = 0; i < queries.length; i++) {
    const visited = new Set<string>();
    res[i] = dfs(queries[i][0], queries[i][1], visited, 1);
  }

  return res;
};

```
## My Notes - 我的笔记


# DFS
思路：对`equation` 中的每一组节点`equation[i]`建立带权的有向无环图，权值为这一组节点相除的值，即`value[i]`。同样的，被除数和除数交换过来也需要建图，权值为`1/value[i]`。
然后dfs 即可。终止条件是 `node === target`。
```typescript
function calcEquation(equations: string[][], values: number[], queries: string[][]): number[] {
  // construst the graph
  const graph: Map<string, [string, number][]> = new Map();

  for (let i = 0; i < equations.length; i++) {
    const zero = graph.get(equations[i][0])
    if (!zero) {
      graph.set(equations[i][0], [[equations[i][1], values[i]]]);
    } else {
      zero.push([equations[i][1], values[i]])
    }

    const one = graph.get(equations[i][1])
    if (!one) {
      graph.set(equations[i][1], [[equations[i][0], 1 / values[i]]]);
    } else {
      one.push([equations[i][0], 1 / values[i]])
    }
  }


  const dfs = (node: string, target: string, visited: Set<string>, value: number) => {
    if (!graph.get(node)) {
      return -1;
    }

    if (node === target) {
      return value;
    }

    const edges = graph.get(node);

    visited.add(node);

    for (let i = 0; i < edges.length; i++) {
      if (visited.has(edges[i][0])) {
        continue;
      }
      const val = dfs(edges[i][0], target, visited, edges[i][1] * value);
      if (val !== -1) {
        return val;
      }
    }

    return -1;
  }

  const res = new Array(queries.length).fill(-1);

  for (let i = 0; i < queries.length; i++) {
    const visited = new Set<string>();
    res[i] = dfs(queries[i][0], queries[i][1], visited, 1);
  }

  return res;
};
```

```python
class Solution:
    def calcEquation(self, equations: List[List[str]], values: List[float], queries: List[List[str]]) -> List[float]:
      # 创建加权有向图
      graph = defaultdict(dict)
      for (a, b), v in zip(equations, values):
         
          graph[a][b] = v
          graph[b][a] = 1 / v

      print(graph)

      def dfs(node, target, visited, value):
          if node not in graph:
              return -1.0
          if node == target:
              return value

          visited.add(node)
          for neighbor, weight in graph[node].items():
              if neighbor not in visited:
                  result = dfs(neighbor, target, visited, value * weight)
                  if result != -1.0:
                      return result
          return -1.0

      # 对每个查询执行DFS
      result = []
      for a, b in queries:
          visited = set()
          result.append(dfs(a, b, visited, 1.0))

      return result
```

# 并查集
官方解法。

