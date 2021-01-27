# 识别名人
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/find-the-celebrity/?utm_source=sc-github-wzz)
 ## 题目描述
 假设你和 `n` 个人在一个聚会中(标记为 `0` 到 `n - 1`)，其中可能存在一个名人。名人的定义是所有其他 `n - 1` 人都认识他/她，但他/她不知道任何一个。
现在你想要找出这个名人是谁或者验证这个名人不存在。你唯一可以做的事情就是提出如下问题：“你好，A，你认识B吗？” 来获取A是否认识B。您需要通过询问尽可能少的问题(以渐近的意义)来找出名人是谁(或验证其不存在)。
你得到一个辅助函数 `bool know(a，b)`，它会告诉你A是否知道B.实现一个函数 `int findCelebrity(n)`，你的函数应该使 `knows` 的调用次数最少。
 ### 样例说明
 **样例1**
```
输入：
2 // 接下来n*(n-1)行
0 knows 1
1 does not know 0
输出： 1
解释：
所有人都认识1，而且1不认识其他人。
```
**样例2**
```
输入：
3 // 接下来n*(n-1)行
0 does not know 1
0 does not know 2
1 knows 0
1 does not know 2
2 knows 0
2 knows 1
输出：0
解释：
所有人都认识0，而且0不认识其他人。
0不认识1，同时1认识0。
2认识所有人，但是1不认识2。
```
 ### 参考代码
 首先loop一遍找到一个人i使得对于所有j(j>=i)都不认识i。
然后再loop一遍判断是否有人不认识i或者i认识某个人。
```java
// version: 高频题班
public class Solution extends Relation {
    /**
     * @param n a party with n people
     * @return the celebrity's label or -1
     */
    public int findCelebrity(int n) {
        // Write your code here
        int ans = 0;
        for (int i = 1; i < n; i++) {
            if (knows(ans, i)) {
                ans = i;
            }
        }

        for (int i = 0; i < n; i++) {
            if (ans != i && knows(ans, i)) {
                return -1;
            }
            if (ans != i && !knows(i, ans)) {
                return -1;
            }
        }
        return ans;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)