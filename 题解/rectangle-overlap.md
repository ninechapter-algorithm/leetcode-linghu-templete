# 矩形重叠
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/rectangle-overlap/?utm_source=sc-github-wzz)
 ## 题目描述
 给定两个矩形，判断这两个矩形是否有重叠。
 ### 样例说明
 **样例 1:**
```
输入 : l1 = [0, 8], r1 = [8, 0], l2 = [6, 6], r2 = [10, 0]
输出 : true
```
**样例 2:**
```
输入 : [0, 8], r1 = [8, 0], l2 = [9, 6], r2 = [10, 0]
输出 : false
```
 ### 参考代码
 判断一下边界即可
```java
/**
 * Definition for a point.
 * class Point {
 *     public int x, y;
 *     public Point() { x = 0; y = 0; }
 *     public Point(int a, int b) { x = a; y = b; }
 * }
 */

public class Solution {
    /**
     * @param l1 top-left coordinate of first rectangle
     * @param r1 bottom-right coordinate of first rectangle
     * @param l2 top-left coordinate of second rectangle
     * @param r2 bottom-right coordinate of second rectangle
     * @return true if they are overlap or false
     */
    public boolean doOverlap(Point l1, Point r1, Point l2, Point r2) {
        // Write your code here
        if (l1.x > r2.x || l2.x > r1.x)
            return false;
    
        if (l1.y < r2.y || l2.y < r1.y)
            return false;
 
        return true;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)