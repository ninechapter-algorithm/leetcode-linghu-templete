# 在大数组中查找
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/search-in-a-big-sorted-array/?utm_source=sc-github-wzz)
 ## 题目描述
 给一个按照升序排序的非负整数数组。这个数组很大以至于你只能通过固定的接口 `ArrayReader.get(k)` 来访问第k个数(或者C++里是ArrayReader->get(k))，并且你也没有办法得知这个数组有多大。

找到给出的整数target第一次出现的位置。你的算法需要在O(logk)的时间复杂度内完成，k为target第一次出现的位置的下标。

如果找不到target，返回-1。
 ### 样例说明
 **样例 1:**

```
输入: [1, 3, 6, 9, 21, ...], target = 3
输出: 1
```

**样例 2:**

```
输入: [1, 3, 6, 9, 21, ...], target = 4
输出: -1
```
 ### 参考代码
 > 该题目有两种思路: 二分和倍增. 其实这两种方法有一些相似之处, 很多时候可以在相同的时空分析下解决同一个问题.

**方法1 倍增:**

首先特判一下首个元素. 然后设定 `idx = 0` 为查找的下标, `jump = 1` 为向后跳跃的长度.

每次循环将 `idx` 向后移动 `jump` 个元素, 并将 `jump` 翻倍. 而如果移动后的位置不小于 `target`, 则 `jump` 缩小至一半.

即我们在保证每次跳跃后的 `idx` 的位置都小于`target`的前提下, 倍增式地跳跃, 以此保证 O(logn) 的时间复杂度.

循环终止的条件就是 `jump == 0`, 就是说, 这时 `idx + 1` 的位置以及不小于 `target` 了 (此时idx位置的仍然是小于target)

也就是说, 到最后`idx`指向的元素是: 最大的小于`target`的元素. 返回答案前判断一下 `idx + 1` 是否 `target` 即可.

---

**方法2 二分:**

二分查找第一个不小于`target`的元素很简单. 但是需要确定二分区间的范围. 此时还是需要倍增地找到右边界.

初始右边界为1, 如果右边界的数小于 `target`, 就将其倍增, 直到右边界不小于`target`.

这时就可以二分查找了.

注意: 越界访问是没有关系的, 因为这个`ArrayReader`在越界访问时, 返回 INT_MAX, 一定不小于 `target`. 而即使是返回 -1 之类的数值, 我们也可以加一个判断搞定.
```java
/////////////// 方法1 倍增

/**
 * Definition of ArrayReader:
 * 
 * public class ArrayReader {
 * public int get(int index) {
 *          // return the number on given index, 
 *          // return 2147483647 if the index is invalid.
 *     }
 * };
 */
public class Solution {
    /*
     * @param reader: An instance of ArrayReader.
     * @param target: An integer
     * @return: An integer which is the first index of target.
     */
    public int searchBigSortedArray(ArrayReader reader, int target) {
        int firstElement = reader.get(0);
        if (firstElement == target) 
            return 0;
        else if (firstElement > target)
            return -1;
        
        int idx = 0, jump = 1;
        while (jump != 0) {
            while (jump != 0 && reader.get(idx + jump) >= target)   // 越界时返回INT_MAX, 必然不小于target
                jump >>= 1;
            idx += jump;
            jump <<= 1;     // 当jump为0时, 左移一位不影响它的值, 不影响循环结束
        }
        
        if (reader.get(idx + 1) == target)
            return idx + 1;
        else
            return -1;
    }
}

/////////////// 方法2 二分

/**
 * Definition of ArrayReader:
 * 
 * public class ArrayReader {
 * public int get(int index) {
 *          // return the number on given index, 
 *          // return 2147483647 if the index is invalid.
 *     }
 * };
 */
public class Solution {
    /*
     * @param reader: An instance of ArrayReader.
     * @param target: An integer
     * @return: An integer which is the first index of target.
     */
    public int searchBigSortedArray(ArrayReader reader, int target) {
        int l = 0, r = 1, mid;
        while (reader.get(r) < target)     // 越界返回INT_MAX, 必然大于target, 所以没有关系
            r <<= 1;
        
        while (l < r) {
            mid = (l + r) >> 1;
            if (reader.get(mid) >= target)
                r = mid;
            else
                l = mid + 1;
        }
        
        if (reader.get(l) == target)
            return l;
        else
            return -1;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)