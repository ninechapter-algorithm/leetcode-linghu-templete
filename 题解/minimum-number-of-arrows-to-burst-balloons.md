# 爆破气球的最小箭头数
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/minimum-number-of-arrows-to-burst-balloons/?utm_source=sc-github-wzz)
 ## 题目描述
 在二维空间中有许多球形气球。 对于每个气球，提供的输入是水平直径的起点和终点坐标。 由于它是水平的，因此y坐标无关紧要，因此直径的起点和终点的x坐标就足够了。 起点总是小于终点。 最多将有10^4个气球。

可以沿x轴从不同点垂直向上发射箭头。 如果xstart≤x≤xend，则坐标为xstart和xend的气球被在x处发射的箭头戳爆。 可以发射的箭头数量没有限制。 一次射击的箭头一直无限地向上移动。 问题是要找到戳破所有气球的最小发射箭头数。
 ### 样例说明
 **样例1**
```
输入:
[[10,16], [2,8], [1,6], [7,12]]
输出:
2
说明：
一种方法是发射一个箭头，例如在x = 6（爆破气球[2,8]和[1,6]），发射另一个箭头在x = 11（爆破其他两个气球）。
```
**样例2**
```
输入:
[[1,2],[3,4],[5,6],[7,8]]
输出:
4
```
 ### 参考代码
 使用贪心算法解决此问题。
我们首先将气球按照end从小到大进行排序，首先将第一个气球的end作为参考。
从左到右遍历，若当前气球的起点小于等于参考点则continue；
若当前气球的起点大于参考点，则将参考点更新为当前气球的终点，同时答案+1。
```java
public class Solution {
    public int findMinArrowShots(int[][] points) {
        if (points == null || points.length == 0) return 0;
        Arrays.sort(points, new IntervalComparator());
        int ans = 1;
        int lastEnd = points[0][1];
        for(int i = 1; i < points.length; i++) {
            if (points[i][0] > lastEnd) {
                ans++;
                lastEnd = points[i][1];
            }
        }
        return ans;
    }
    
    class IntervalComparator implements Comparator<int[]> {
        public int compare(int[] a, int[] b) {
            return a[1] - b[1];
        }
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)