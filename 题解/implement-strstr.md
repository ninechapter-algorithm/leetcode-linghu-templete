# 字符串查找
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/implement-strstr/?utm_source=sc-github-wzz)
 ## 题目描述
 对于一个给定的 source 字符串和一个 target 字符串，你应该在 source 字符串中找出 target 字符串出现的第一个位置(从0开始)。如果不存在，则返回 `-1`。
 ### 样例说明
 **样例  1:**

```
输入: source = "source" ， target = "target"
输出:-1	
样例解释: 如果source里没有包含target的内容，返回-1
```

**样例 2:**

```
输入: source = "abcdabcdefg" ，target = "bcd"
输出: 1	
样例解释: 如果source里包含target的内容，返回target在source里第一次出现的位置
```


 ### 参考代码
 Implement strStr().

Returns a pointer to the first occurrence of needle in haystack, or null if needle is not part of haystack.
```java
class Solution {
    /**
     * Returns a index to the first occurrence of target in source,
     * or -1  if target is not part of source.
     * @param source string to be scanned.
     * @param target string containing the sequence of characters to match.
     */
    public int strStr(String source, String target) {
        if (source == null || target == null) {
            return -1;
        }
        
        for (int i = 0; i < source.length() - target.length() + 1; i++) {
            int j = 0;
            for (j = 0; j < target.length(); j++) {
                if (source.charAt(i + j) != target.charAt(j)) {
                    break;
                }
            }
            // finished loop, target found
            if (j == target.length()) {
                return i;
            }
        }
        return -1;
    }
}

```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)