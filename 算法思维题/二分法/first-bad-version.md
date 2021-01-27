# 第一个错误的代码版本
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/first-bad-version/?utm_source=sc-github-wzz)
 ## 题目描述
 代码库的版本号是从 1 到 *n* 的整数。某一天，有人提交了错误版本的代码，因此造成自身及之后版本的代码在单元测试中均出错。请找出第一个错误的版本号。

你可以通过 `isBadVersion` 的接口来判断版本号 version 是否在单元测试中出错，具体接口详情和调用方法请见代码的注释部分。
 ### 样例说明
 ```
n = 5:

    isBadVersion(3) -> false
    isBadVersion(5) -> true
    isBadVersion(4) -> true

因此可以确定第四个版本是第一个错误版本。
```
 ### 参考代码
 使用二分答案方法，即可定位出第一个错误版本。
```java
/**
 * public class GitRepo {
 *     public static boolean isBadVersion(int k);
 * }
 * you can use GitRepo.isBadVersion(k) to judge whether 
 * the kth code version is bad or not.
*/
class Solution {
    /**
     * @param n: An integers.
     * @return: An integer which is the first bad version.
     */
    public int findFirstBadVersion(int n) {
        int start = 1, end = n;
        while (start + 1 < end) {
            int mid = start + (end - start) / 2;
            if (SVNRepo.isBadVersion(mid)) {
                end = mid;
            } else {
                start = mid;
            }
        }
            
        if (SVNRepo.isBadVersion(start)) {
            return start;
        }
        return end;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)