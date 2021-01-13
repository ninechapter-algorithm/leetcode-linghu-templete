# 攀爬字符串
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/scramble-string/?utm_source=sc-github-wzz)
 ## 题目描述
 给定一个字符串 `s1`, 将其递归地分割成两个非空子字符串, 然后可以得到一棵二叉树.

下面是 `s1 = "great"` 可能得到的一棵二叉树: 

```txt
      great
     /    \
    gr    eat
   / \    /  \
  g   r  e   at
             / \
            a   t
```

在攀爬字符串的过程中, 我们可以选择其中任意一个非叶节点, 交换该节点的两个子节点.

例如，我们选择了 `"gr"` 节点, 并将该节点的两个子节点进行交换, 并且将祖先节点对应的子串部分也交换, 最终得到了 `"rgeat"`. 我们认为 `"rgeat"` 是 `"great"` 的一个攀爬字符串.

```txt
      rgeat
     /    \
    rg    eat
   / \    /  \
  r   g  e   at
             / \
            a   t
```

类似地, 如果我们继续将其节点 `"eat"` 和 `"at"` 的子节点交换, 又可以得到 `"great"` 的一个攀爬字符串 `"rgtae"`.

```txt
     rgtae
     /    \
    rg    tae
   / \    /  \
  r   g  ta   e
         / \
        t   a
```

给定两个相同长度的字符串 `s1` 和 `s2`，判断 `s2` 是否为 `s1` 的攀爬字符串.
 ### 样例说明
 **样例 1:**

```
输入: s1 = "great", s2 = "rgeat"
输出: true
解释: 如同上面描述的.
```

**样例 2:**

```
输入: s1 = "a", s2 = "b"
输出: false
```
 ### 参考代码
 如果组成 s1 和 s2 的每种字符的数量不同, 可以直接判定为 `false`, 例如样例2的 "a" 和 "b". 以及两个字符串长度不相同也可以直接返回 `false`.

这道题目的重点实际上是找到构造二叉树的方式. 二叉树的构造决定了 `s1` 的哪些部分可以交换位置来得到新的字符串. 下面提供了多个版本算法的代码, 这里只介绍动态规划的思路:

设定状态: `f[l1][r1][l2][r2]` 表示是否可以由 `s1` 的[l1, r1]的子串攀爬得到 `s2` 的[l2, r2]的子串. 决策便是从哪里分割 `s1`, 所以我们枚举分割的点, 于是达到了子问题.

不过需要注意的是, 由于二叉树的子节点可以被交换, 所以 `s2` 可能是被交换过的, 所以完整的状态转移方程是:

```C++
// 枚举k, 表示从 s1的 [l1, r1] 的第k个字符后分割, 只要有其中一种分割可以得到 s2 即可, 因此是在枚举的 k 中取 或运算
f[l1][r1][l2][r2] = OR (f[l1][l1 + k - 1][l2][l2 + k - 1] && f[l1 + k][r1][l2 + k][r2]) // 该节点的两个子节点没有交换过
                    OR (f[l1][l1 + k - 1][r2 - k + 1][r2] && f[l1 + k][r1][l2][r2 - k]) // 该节点的两个子节点交换过
```

边界状态即: `f[l1][l1][l2][l2] = (s1[l1] == s2[l2])`

注意到 r1 - l1 == r2 - l2, 所以这个四维数组可以被优化掉一维.
```python
class Solution:
    def isScramble(self, s1, s2):
        n = len(s1)
        # f[i][j][k] 表示 s1[i : i + k] 攀爬能否得到 s2[j : j + k]
        f = [[[False] * (n + 1) for _ in range(n)] for _ in range(n)]
        for i in range(n):
            for j in range(n):
                f[i][j][1] = s1[i] == s2[j]
        for k in range(2, n + 1):
            for i in range(0, n - k + 1):
                for j in range(0, n - k + 1):
                    for t in range(1, k):
                        if f[i][j][t] and f[i + t][j + t][k - t]:
                            f[i][j][k] = True
                            break
                        if f[i][j + k - t][t] and f[i + t][j][k - t]:
                            f[i][j][k] = True
                            break
        return f[0][0][n]
        
class Solution:
    def isScramble(self, s1, s2):
        if len(s1) != len(s2):
            return False
        if s1 == s2:
            return True
        if sorted(list(s1)) != sorted(list(s2)):
            return False
        length = len(s1)
        for i in range(1, length):
            if self.isScramble(s1[:i], s2[:i]) and self.isScramble(s1[i:], s2[i:]):
                return True
            if self.isScramble(s1[:i], s2[length-i:]) and self.isScramble(s1[i:], s2[:length-i]):
                return True
        return False
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)