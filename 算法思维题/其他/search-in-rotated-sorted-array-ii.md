# 搜索旋转排序数组 II
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/search-in-rotated-sorted-array-ii/?utm_source=sc-github-wzz)
 ## 题目描述
 <p>跟进“搜索旋转排序数组”，假如有重复元素又将如何？</p><p><i>是否会影响运行时间复杂度？</i></p><p><i>如何影响？</i></p><p><i>为何会影响？</i></p><p>写出一个函数判断给定的目标值是否出现在数组中。</p>
 ### 样例说明
 例1:
```
输入:
[]
1
输出:
false
```
例2:
```
输入:
[3,4,4,5,7,0,1,2]
4
输出:
true
```

 ### 参考代码
 由于出现重复元素，故不能使用二分法。
所以暴力比较即可。
```java
public class Solution {
    // 这个问题在面试中不会让实现完整程序
    // 只需要举出能够最坏情况的数据是 [1,1,1,1... 1] 里有一个0即可。
    // 在这种情况下是无法使用二分法的，复杂度是O(n)
    // 因此写个for循环最坏也是O(n)，那就写个for循环就好了
    //  如果你觉得，不是每个情况都是最坏情况，你想用二分法解决不是最坏情况的情况，那你就写一个二分吧。
    //  反正面试考的不是你在这个题上会不会用二分法。这个题的考点是你想不想得到最坏情况。
    public boolean search(int[] A, int target) {
        for (int i = 0; i < A.length; i ++) {
            if (A[i] == target) {
                return true;
            }
        }
        return false;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)