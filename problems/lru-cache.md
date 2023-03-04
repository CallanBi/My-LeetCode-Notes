
# 146. LRU Cache - LRU 缓存

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Design-设计-blue.svg">   <img src="https://img.shields.io/badge/Hash Table-哈希表-blue.svg">   <img src="https://img.shields.io/badge/Linked List-链表-blue.svg">   <img src="https://img.shields.io/badge/Doubly Linked List-双向链表-blue.svg">  


## Description - 题目描述

### EN:
<p>Design a data structure that follows the constraints of a <strong><a href="https://en.wikipedia.org/wiki/Cache_replacement_policies#LRU" target="_blank">Least Recently Used (LRU) cache</a></strong>.</p>

<p>Implement the <code>LRUCache</code> class:</p>

<ul>
	<li><code>LRUCache(int capacity)</code> Initialize the LRU cache with <strong>positive</strong> size <code>capacity</code>.</li>
	<li><code>int get(int key)</code> Return the value of the <code>key</code> if the key exists, otherwise return <code>-1</code>.</li>
	<li><code>void put(int key, int value)</code> Update the value of the <code>key</code> if the <code>key</code> exists. Otherwise, add the <code>key-value</code> pair to the cache. If the number of keys exceeds the <code>capacity</code> from this operation, <strong>evict</strong> the least recently used key.</li>
</ul>

<p>The functions <code>get</code> and <code>put</code> must each run in <code>O(1)</code> average time complexity.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input</strong>
[&quot;LRUCache&quot;, &quot;put&quot;, &quot;put&quot;, &quot;get&quot;, &quot;put&quot;, &quot;get&quot;, &quot;put&quot;, &quot;get&quot;, &quot;get&quot;, &quot;get&quot;]
[[2], [1, 1], [2, 2], [1], [3, 3], [2], [4, 4], [1], [3], [4]]
<strong>Output</strong>
[null, null, null, 1, null, -1, null, -1, 3, 4]

<strong>Explanation</strong>
LRUCache lRUCache = new LRUCache(2);
lRUCache.put(1, 1); // cache is {1=1}
lRUCache.put(2, 2); // cache is {1=1, 2=2}
lRUCache.get(1);    // return 1
lRUCache.put(3, 3); // LRU key was 2, evicts key 2, cache is {1=1, 3=3}
lRUCache.get(2);    // returns -1 (not found)
lRUCache.put(4, 4); // LRU key was 1, evicts key 1, cache is {4=4, 3=3}
lRUCache.get(1);    // return -1 (not found)
lRUCache.get(3);    // return 3
lRUCache.get(4);    // return 4
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= capacity &lt;= 3000</code></li>
	<li><code>0 &lt;= key &lt;= 10<sup>4</sup></code></li>
	<li><code>0 &lt;= value &lt;= 10<sup>5</sup></code></li>
	<li>At most <code>2 * 10<sup>5</sup></code> calls will be made to <code>get</code> and <code>put</code>.</li>
</ul>


### ZH-CN:
<div class="title__3Vvk">请你设计并实现一个满足&nbsp; <a href="https://baike.baidu.com/item/LRU" target="_blank">LRU (最近最少使用) 缓存</a> 约束的数据结构。</div>

<div class="title__3Vvk">实现 <code>LRUCache</code> 类：</div>

<div class="original__bRMd">
<div>
<ul>
	<li><code>LRUCache(int capacity)</code> 以 <strong>正整数</strong> 作为容量&nbsp;<code>capacity</code> 初始化 LRU 缓存</li>
	<li><code>int get(int key)</code> 如果关键字 <code>key</code> 存在于缓存中，则返回关键字的值，否则返回 <code>-1</code> 。</li>
	<li><code>void put(int key, int value)</code>&nbsp;如果关键字&nbsp;<code>key</code> 已经存在，则变更其数据值&nbsp;<code>value</code> ；如果不存在，则向缓存中插入该组&nbsp;<code>key-value</code> 。如果插入操作导致关键字数量超过&nbsp;<code>capacity</code> ，则应该 <strong>逐出</strong> 最久未使用的关键字。</li>
</ul>

<p>函数 <code>get</code> 和 <code>put</code> 必须以 <code>O(1)</code> 的平均时间复杂度运行。</p>
</div>
</div>

<p>&nbsp;</p>

<p><strong>示例：</strong></p>

<pre>
<strong>输入</strong>
["LRUCache", "put", "put", "get", "put", "get", "put", "get", "get", "get"]
[[2], [1, 1], [2, 2], [1], [3, 3], [2], [4, 4], [1], [3], [4]]
<strong>输出</strong>
[null, null, null, 1, null, -1, null, -1, 3, 4]

<strong>解释</strong>
LRUCache lRUCache = new LRUCache(2);
lRUCache.put(1, 1); // 缓存是 {1=1}
lRUCache.put(2, 2); // 缓存是 {1=1, 2=2}
lRUCache.get(1);    // 返回 1
lRUCache.put(3, 3); // 该操作会使得关键字 2 作废，缓存是 {1=1, 3=3}
lRUCache.get(2);    // 返回 -1 (未找到)
lRUCache.put(4, 4); // 该操作会使得关键字 1 作废，缓存是 {4=4, 3=3}
lRUCache.get(1);    // 返回 -1 (未找到)
lRUCache.get(3);    // 返回 3
lRUCache.get(4);    // 返回 4
</pre>

<p>&nbsp;</p>

<p><strong>提示：</strong></p>

<ul>
	<li><code>1 &lt;= capacity &lt;= 3000</code></li>
	<li><code>0 &lt;= key &lt;= 10000</code></li>
	<li><code>0 &lt;= value &lt;= 10<sup>5</sup></code></li>
	<li>最多调用 <code>2 * 10<sup>5</sup></code> 次 <code>get</code> 和 <code>put</code></li>
</ul>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/lru-cache/description/)  -  [LeetCode-CN](https://leetcode.cn/problems/lru-cache/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| typescript  | 568 ms | 99.1 MB | 2022/09/16 10:54 |

```typescript

type DBLinkNode = {
  prev: DBLinkNode | null;
  next: DBLinkNode | null;
  key: number;
  val: number;
}

class LRUCache {
  private static cap: number;
  private static len: number;
  private static DBLink: DBLinkNode;
  private static cache: Map<number, DBLinkNode>;
  private static head: DBLinkNode;
  private static tail: DBLinkNode;
  constructor(capacity: number) {
    LRUCache.cap = capacity;
    LRUCache.len = 0;
    // init tail guard and head guard
    LRUCache.DBLink = {
      prev: null,
      next: {
        prev: null,
        next: null,
        key: -1,
        val: -1,
      },
      key: -1,
      val: -1,
    };

    LRUCache.DBLink.next.prev = LRUCache.DBLink;

    LRUCache.head = LRUCache.DBLink;

    LRUCache.tail = LRUCache.DBLink.next;

    LRUCache.cache = new Map<number, DBLinkNode>();
  }

  get(key: number): number {
    if (!LRUCache.cache.has(key)) {
      return -1;
    }

    const node = LRUCache.cache.get(key);

    this.moveToHead(node);

    return node.val;
  }

  put(key: number, value: number): void {
    if (LRUCache.cache.has(key)) {
      const node = LRUCache.cache.get(key);
      node.val = value;
      this.moveToHead(node);
      return;
    }

    if (LRUCache.len + 1 > LRUCache.cap) {
      this.removeTail();
    }

    this.addToHead({
      prev: null,
      next: null,
      key,
      val: value,
    } as DBLinkNode);
  }

  moveToHead(node: DBLinkNode): void {
    node.prev.next = node.next;
    node.next.prev = node.prev;

    LRUCache.len -= 1;

    this.addToHead(node);
  }

  addToHead(node: DBLinkNode): void {
    node.prev = LRUCache.head;

    node.next = LRUCache.head.next;

    LRUCache.head.next.prev = node;

    LRUCache.head.next = node;

    if (!LRUCache.cache.has(node.key)) {
      LRUCache.cache.set(node.key, node);
    }

    LRUCache.len += 1;
  }

  removeTail(): void {
    let shouldDeleted = LRUCache.tail.prev;

    shouldDeleted.next = null;

    LRUCache.tail.prev = shouldDeleted.prev;

    LRUCache.tail.prev.next = LRUCache.tail;

    LRUCache.cache.delete(shouldDeleted.key);

    shouldDeleted = null;

    LRUCache.len -= 1;
  }
}

/**
 * Your LRUCache object will be ins tantiated and called as such:
 * var obj = new LRUCache(capacity)
 * var param_1 = obj.get(key)
 * obj.put(key,value)
 */

```
## My Notes - 我的笔记


No notes

