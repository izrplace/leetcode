# [268. 丢失的数字](https://leetcode-cn.com/problems/missing-number)

[English Version](/solution/0200-0299/0268.Missing%20Number/README_EN.md)

## 题目描述

<!-- 这里写题目描述 -->

<p>给定一个包含 <code>[0, n]</code> 中 <code>n</code> 个数的数组 <code>nums</code> ，找出 <code>[0, n]</code> 这个范围内没有出现在数组中的那个数。</p>

<p> </p>

<p><strong>进阶：</strong></p>

<ul>
	<li>你能否实现线性时间复杂度、仅使用额外常数空间的算法解决此问题?</li>
</ul>

<p> </p>

<p><strong>示例 1：</strong></p>

<pre>
<strong>输入：</strong>nums = [3,0,1]
<strong>输出：</strong>2
<b>解释：</b>n = 3，因为有 3 个数字，所以所有的数字都在范围 [0,3] 内。2 是丢失的数字，因为它没有出现在 nums 中。</pre>

<p><strong>示例 2：</strong></p>

<pre>
<strong>输入：</strong>nums = [0,1]
<strong>输出：</strong>2
<b>解释：</b>n = 2，因为有 2 个数字，所以所有的数字都在范围 [0,2] 内。2 是丢失的数字，因为它没有出现在 nums 中。</pre>

<p><strong>示例 3：</strong></p>

<pre>
<strong>输入：</strong>nums = [9,6,4,2,3,5,7,0,1]
<strong>输出：</strong>8
<b>解释：</b>n = 9，因为有 9 个数字，所以所有的数字都在范围 [0,9] 内。8 是丢失的数字，因为它没有出现在 nums 中。</pre>

<p><strong>示例 4：</strong></p>

<pre>
<strong>输入：</strong>nums = [0]
<strong>输出：</strong>1
<b>解释：</b>n = 1，因为有 1 个数字，所以所有的数字都在范围 [0,1] 内。1 是丢失的数字，因为它没有出现在 nums 中。</pre>

<p> </p>

<p><strong>提示：</strong></p>

<ul>
	<li><code>n == nums.length</code></li>
	<li><code>1 <= n <= 10<sup>4</sup></code></li>
	<li><code>0 <= nums[i] <= n</code></li>
	<li><code>nums</code> 中的所有数字都 <strong>独一无二</strong></li>
</ul>

## 解法

<!-- 这里可写通用的实现逻辑 -->

异或求解。两个相同的数异或的结果为 0。

也可以用数学求解。求出 `[0..n]` 的和，减去数组中所有数的和，就得到了缺失的数字。

<!-- tabs:start -->

### **Python3**

<!-- 这里可写当前语言的特殊实现逻辑 -->

```python
class Solution:
    def missingNumber(self, nums: List[int]) -> int:
        res = len(nums)
        for i, v in enumerate(nums):
            res ^= (i ^ v)
        return res
```

### **Java**

<!-- 这里可写当前语言的特殊实现逻辑 -->

-   异或

```java
class Solution {
    public int missingNumber(int[] nums) {
        int res = nums.length;
        for (int i = 0, n = res; i < n; ++i) {
            res ^= (i ^ nums[i]);
        }
        return res;
    }
}
```

-   数学

```java
class Solution {
    public int missingNumber(int[] nums) {
        int res = nums.length;
        for (int i = 0, n = res; i < n; ++i) {
            res += (i - nums[i]);
        }
        return res;
    }
}
```

### **C++**

```cpp
class Solution {
public:
    int missingNumber(vector<int>& nums) {
        int n = nums.size();
        int res = n;
        for (int i = 0; i < n; ++i) {
            res ^= (i ^ nums[i]);
        }
        return res;
    }
};
```

### **Go**

```go
func missingNumber(nums []int) int {
	n := len(nums)
	res := n
	for i := 0; i < n; i++ {
		res ^= (i ^ nums[i])
	}
	return res
}
```

### **...**

```

```

<!-- tabs:end -->
