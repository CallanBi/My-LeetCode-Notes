
# 152. Maximum Product Subarray - 乘积最大子数组

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Array-数组-blue.svg">   <img src="https://img.shields.io/badge/Dynamic Programming-动态规划-blue.svg">  


## Description - 题目描述

### EN:
<p>Given an integer array <code>nums</code>, find a <span data-keyword="subarray-nonempty">subarray</span> that has the largest product, and return <em>the product</em>.</p>

<p>The test cases are generated so that the answer will fit in a <strong>32-bit</strong> integer.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input:</strong> nums = [2,3,-2,4]
<strong>Output:</strong> 6
<strong>Explanation:</strong> [2,3] has the largest product 6.
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre>
<strong>Input:</strong> nums = [-2,0,-1]
<strong>Output:</strong> 0
<strong>Explanation:</strong> The result cannot be 2, because [-2,-1] is not a subarray.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= nums.length &lt;= 2 * 10<sup>4</sup></code></li>
	<li><code>-10 &lt;= nums[i] &lt;= 10</code></li>
	<li>The product of any prefix or suffix of <code>nums</code> is <strong>guaranteed</strong> to fit in a <strong>32-bit</strong> integer.</li>
</ul>


### ZH-CN:
<p>给你一个整数数组 <code>nums</code>&nbsp;，请你找出数组中乘积最大的非空连续子数组（该子数组中至少包含一个数字），并返回该子数组所对应的乘积。</p>

<p>测试用例的答案是一个&nbsp;<strong>32-位</strong> 整数。</p>

<p><strong>子数组</strong> 是数组的连续子序列。</p>

<p>&nbsp;</p>

<p><strong>示例 1:</strong></p>

<pre>
<strong>输入:</strong> nums = [2,3,-2,4]
<strong>输出:</strong> <code>6</code>
<strong>解释:</strong>&nbsp;子数组 [2,3] 有最大乘积 6。
</pre>

<p><strong>示例 2:</strong></p>

<pre>
<strong>输入:</strong> nums = [-2,0,-1]
<strong>输出:</strong> 0
<strong>解释:</strong>&nbsp;结果不能为 2, 因为 [-2,-1] 不是子数组。</pre>

<p>&nbsp;</p>

<p><strong>提示:</strong></p>

<ul>
	<li><code>1 &lt;= nums.length &lt;= 2 * 10<sup>4</sup></code></li>
	<li><code>-10 &lt;= nums[i] &lt;= 10</code></li>
	<li><code>nums</code> 的任何前缀或后缀的乘积都 <strong>保证</strong>&nbsp;是一个 <strong>32-位</strong> 整数</li>
</ul>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/maximum-product-subarray/description/)  -  [LeetCode-CN](https://leetcode.cn/problems/maximum-product-subarray/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| golang  | 4 ms | 3.8 MB | 2023/01/09 21:55 |

```golang

func maxProduct(nums []int) int {
    if len(nums) == 1 {
        return nums[0]
    }

    dpMax := make([]int, len(nums), len(nums))
    dpMin := make([]int, len(nums), len(nums))

    dpMax[0] = nums[0]
    dpMin[0] = nums[0]

    for i := 1; i < len(nums); i++ {
        dpMax[i] = max(dpMin[i - 1] * nums[i], dpMax[i - 1] * nums[i], nums[i])
        dpMin[i] = min(dpMin[i - 1] * nums[i], dpMax[i - 1] * nums[i], nums[i])
    }

    return max(dpMax...)
}

func max(params ...int) int {
    maxNum := -9999999999999999;
    for _, e := range params {
        if e > maxNum {
            maxNum = e
        }
    }
    return maxNum
}

func min(params ...int) int {
    minNum := 99999999999999999;
    for _, e := range params {
        if e < minNum {
            minNum = e
        }
    }
    return minNum
}

```
## My Notes - 我的笔记


No notes

