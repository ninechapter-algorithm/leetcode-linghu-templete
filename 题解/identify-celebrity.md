# identify celebrity
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/identify-celebrity/?utm_source=sc-github-wzz)
 ## 题目描述
 1786
 ### 样例说明
 1786
 ### 参考代码
 ```java
/* The knows API is defined in the parent class Relation.
      boolean knows(int a, int b); */

public class Solution extends Relation {
    /**
     * @param n a party with n people
     * @return the celebrity's label or -1
     */
    public int findCelebrity(int n) {
        // Write your code here
        int candidate = 0;
        for(int i = 1; i < n; i++) {
            if (knows(candidate, i)) {
                candidate = i;
            }
        }
        for(int i = 0; i < candidate; i++) {
            if(knows(candidate, i) || !knows(i, candidate)) {
                return -1;
            }
        }
        for(int i = candidate + 1; i < n; i++) {
            if(!knows(i, candidate)) {
                return -1;
            }
        }
        return candidate;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)