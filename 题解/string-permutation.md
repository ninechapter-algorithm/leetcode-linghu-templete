# 字符串置换
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/string-permutation/?utm_source=sc-github-wzz)
 ## 题目描述
 给定两个字符串，请设计一个方法来判定其中一个字符串是否为另一个字符串的置换。

置换的意思是，通过改变顺序可以使得两个字符串相等。
 ### 样例说明
 
 ### 参考代码
 统计字符数量，组成成分一致即可置换得到。
```java
public class Solution {
    /**
     * @param A a string
     * @param B a string
     * @return a boolean
     */
    public boolean stringPermutation(String A, String B) {
        // Write your code here
        int[] cnt = new int[1000];
        for (int i = 0; i < A.length(); ++i)
            cnt[(int)A.charAt(i)] += 1;
        for (int i = 0; i < B.length(); ++i)
            cnt[(int)B.charAt(i)] -= 1;
        for (int i = 0; i < 1000; ++i)
            if (cnt[i] != 0)
                return false;
        return true;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)