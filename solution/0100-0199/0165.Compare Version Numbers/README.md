# [165. 比较版本号](https://leetcode-cn.com/problems/compare-version-numbers)

[English Version](/solution/0100-0199/0165.Compare%20Version%20Numbers/README_EN.md)

## 题目描述

<!-- 这里写题目描述 -->

<p>给你两个版本号 <code>version1</code> 和 <code>version2</code> ，请你比较它们。</p>

<p>版本号由一个或多个修订号组成，各修订号由一个 <code>'.'</code> 连接。每个修订号由 <strong>多位数字</strong> 组成，可能包含 <strong>前导零</strong> 。每个版本号至少包含一个字符。修订号从左到右编号，下标从 0 开始，最左边的修订号下标为 0 ，下一个修订号下标为 1 ，以此类推。例如，<code>2.5.33</code> 和 <code>0.1</code> 都是有效的版本号。</p>

<p>比较版本号时，请按从左到右的顺序依次比较它们的修订号。比较修订号时，只需比较 <strong>忽略任何前导零后的整数值</strong> 。也就是说，修订号 <code>1</code> 和修订号 <code>001</code> <strong>相等 </strong>。如果版本号没有指定某个下标处的修订号，则该修订号视为 <code>0</code> 。例如，版本 <code>1.0</code> 小于版本 <code>1.1</code> ，因为它们下标为 <code>0</code> 的修订号相同，而下标为 <code>1</code> 的修订号分别为 <code>0</code> 和 <code>1</code> ，<code>0 < 1</code> 。</p>

<p>返回规则如下：</p>

<ul>
	<li>如果 <code><em>version1 </em>> <em>version2</em></code> 返回 <code>1</code>，</li>
	<li>如果 <code><em>version1 </em>< <em>version2</em></code> 返回 <code>-1</code>，</li>
	<li>除此之外返回 <code>0</code>。</li>
</ul>

<p> </p>

<p><strong>示例 1：</strong></p>

<pre>
<strong>输入：</strong>version1 = "1.01", version2 = "1.001"
<strong>输出：</strong>0
<strong>解释：</strong>忽略前导零，"01" 和 "001" 都表示相同的整数 "1"
</pre>

<p><strong>示例 2：</strong></p>

<pre>
<strong>输入：</strong>version1 = "1.0", version2 = "1.0.0"
<strong>输出：</strong>0
<strong>解释：</strong>version1 没有指定下标为 2 的修订号，即视为 "0"
</pre>

<p><strong>示例 3：</strong></p>

<pre>
<strong>输入：</strong>version1 = "0.1", version2 = "1.1"
<strong>输出：</strong>-1
<strong>解释：</strong>version1 中下标为 0 的修订号是 "0"，version2 中下标为 0 的修订号是 "1" 。0 < 1，所以 version1 < version2
</pre>

<p><strong>示例 4：</strong></p>

<pre>
<strong>输入：</strong>version1 = "1.0.1", version2 = "1"
<strong>输出：</strong>1
</pre>

<p><strong>示例 5：</strong></p>

<pre>
<strong>输入：</strong>version1 = "7.5.2.4", version2 = "7.5.3"
<strong>输出：</strong>-1
</pre>

<p> </p>

<p><strong>提示：</strong></p>

<ul>
	<li><code>1 <= version1.length, version2.length <= 500</code></li>
	<li><code>version1</code> 和 <code>version2</code> 仅包含数字和 <code>'.'</code></li>
	<li><code>version1</code> 和 <code>version2</code> 都是 <strong>有效版本号</strong></li>
	<li><code>version1</code> 和 <code>version2</code> 的所有修订号都可以存储在 <strong>32 位整数</strong> 中</li>
</ul>

## 解法

<!-- 这里可写通用的实现逻辑 -->

**1. 字符串分割**：分割两个字符串，比较对应的修订号。

**2. 双指针**。

<!-- tabs:start -->

### **Python3**

<!-- 这里可写当前语言的特殊实现逻辑 -->

双指针。

```python
class Solution:
    def compareVersion(self, version1: str, version2: str) -> int:
        i, j, m, n = 0, 0, len(version1), len(version2)
        while i < m or j < n:
            a = b = 0
            while i < m and version1[i] != '.':
                a = a * 10 + int(version1[i])
                i += 1
            while j < n and version2[j] != '.':
                b = b * 10 + int(version2[j])
                j += 1
            if a != b:
                return -1 if a < b else 1
            i += 1
            j += 1
        return 0
```

### **Java**

<!-- 这里可写当前语言的特殊实现逻辑 -->

```java
class Solution {
    public int compareVersion(String version1, String version2) {
        for (int i = 0, j = 0; i < version1.length() || j < version2.length(); ++i, ++j) {
            int a = 0, b = 0;
            while (i < version1.length() && version1.charAt(i) != '.') {
                a = a * 10 + version1.charAt(i++) - '0';
            }
            while (j < version2.length() && version2.charAt(j) != '.') {
                b = b * 10 + version2.charAt(j++) - '0';
            }
            if (a != b) {
                return a < b ? -1 : 1;
            }
        }
        return 0;
    }
}
```

### **TypeScript**

```ts
function compareVersion(version1: string, version2: string): number {
    let v1 = version1.split('.'),
        v2 = version2.split('.');
    for (let i = 0; i < Math.max(v1.length, v2.length); i++) {
        let c1 = Number(v1[i] || 0),
            c2 = Number(v2[i] || 0);
        if (c1 > c2) return 1;
        if (c1 < c2) return -1;
    }
    return 0;
}
```

### **C++**

```cpp
class Solution {
public:
    int compareVersion(string version1, string version2) {
        for (int i = 0, j = 0; i < version1.size() || j < version2.size(); ++i, ++j)
        {
            int a = 0, b = 0;
            while (i < version1.size() && version1[i] != '.')
                a = a * 10 + version1[i++] - '0';
            while (j < version2.size() && version2[j] != '.')
                b = b * 10 + version2[j++] - '0';
            if (a != b)
                return a < b ? -1 : 1;
        }
        return 0;
    }
};
```

### **Go**

```go
func compareVersion(version1 string, version2 string) int {
	for i, j := 0, 0; i < len(version1) || j < len(version2); i, j = i+1, j+1 {
		a, b := 0, 0
		for i < len(version1) && version1[i] != '.' {
			a = a*10 + int(version1[i]-'0')
			i++
		}
		for j < len(version2) && version2[j] != '.' {
			b = b*10 + int(version2[j]-'0')
			j++
		}
		if a < b {
			return -1
		}
		if a > b {
			return 1
		}
	}
	return 0
}
```

### **...**

```

```

<!-- tabs:end -->
