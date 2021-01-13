# 通过面试
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/pass-interview/?utm_source=sc-github-wzz)
 ## 题目描述
 给出面试者的性别和面试成绩，判断求职者是否通过面试。

* 如果面试者是男性，那么面试成绩必须大于等于4分。
* 如果面试者是女性，那么面试成绩必须大于等于3分。

参数sex是boolean类型，sex为true时，代表求职者是女性，因为女人永远都是对的。相反sex为false时，代表求职者为男性，因为男人永远都是错的。
 ### 样例说明
 
 ### 参考代码
 ```java
public class Solution {
    /**
     * @param sex the sex of a candidate
     * @param score the interview score of a candidate
     * @return a boolean
     */
    public boolean passInterview(boolean sex, double score) {
        if (sex) {
            return score >= 3;
        }
        return score >= 4;
    }
}

```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)