# 三角形计数
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/triangle-count/?utm_source=sc-github-wzz)
 ## 题目描述
 给定一个整数数组，在该数组中，寻找三个数，分别代表三角形三条边的长度，问，可以寻找到多少组这样的三个数来组成三角形？
 ### 样例说明
 **样例 1:**

```
输入: [3, 4, 6, 7]
输出: 3
解释:
可以组成的是 (3, 4, 6), 
           (3, 6, 7),
           (4, 6, 7)
```

**样例 2:**

```
输入: [4, 4, 4, 4]
输出: 4
解释:
任何三个数都可以构成三角形
所以答案为 C(3, 4) = 4
```
 ### 参考代码
 使用双指针算法。
for 循环最大边的位置 i，接下来的任务就是在 0~i-1 之间找到两数之和 > S[i]
```
[[python]]
class Solution:
    """
    @param S: A list of integers
    @return: An integer
    """
    def triangleCount(self, S):
        S.sort()
        
        ans = 0
        for i in range(len(S)):
            left, right = 0, i - 1
            while left < right:
                if S[left] + S[right] > S[i]:
                    ans += right - left
                    right -= 1
                else:
                    left += 1
        return ans
[[java]]
public class Solution {
    /**
     * @param S: A list of integers
     * @return: An integer
     */
    public int triangleCount(int S[]) {
        int left = 0, right = S.length - 1;
        int ans = 0;
        Arrays.sort(S);
        for (int i = 0; i < S.length; i++) {
            left = 0;
            right = i - 1;
            while (left < right) {
                if (S[left] + S[right] > S[i]) {
                    ans = ans + (right - left);
                    right --;
                } else {
                    left ++;
                }
            }
        }
        return ans;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)