# 回旋镖的数量
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/number-of-boomerangs/?utm_source=sc-github-wzz)
 ## 题目描述
 在平面中给定n个点，每一对点都是不同的，“回旋镖”是一个点的的元组 `(i, j, k)`，其中 `i` 和 `j` 之间的距离与`i`和`k`之间的距离相同 **（元组的顺序是重要的）**。

找到回旋镖的数量。 您可以假设n最多为**500**并且点的坐标都在  **[-10000, 10000]** （包括）范围内。


 ### 样例说明
 ```
输入:
[[0,0],[1,0],[2,0]]

输出:
2

说明：
两个回旋镖是[[1,0], [0,0], [2,0]]和[[1,0], [2,0], [0,0]]
```
 ### 参考代码
 两层for循环遍历每两个点，计算两点之间距离，以及可以构成该距离的的个数。
用hash表记录Map<distance, count>
则该距离下可构成回旋镖的个数为count * (count - 1)
```java
public class Solution {
    private int getDistance(int[] a, int[] b) {
        int dx = a[0] - b[0];
        int dy = a[1] - b[1];
        return dx * dx + dy * dy;
    }
    
    public int numberOfBoomerangs(int[][] points) {
        if (points == null) {
            return 0;
        }
        int ans = 0;
        for (int i = 0; i < points.length; i++) {
            Map<Integer, Integer> disCount = new HashMap<>();
            for (int j = 0; j < points.length; j++) {
                if (i == j) {
                    continue;
                }
                int distance = getDistance(points[i], points[j]);
                int count = disCount.getOrDefault(distance, 0);
                disCount.put(distance, count + 1);
            }
            for (int count : disCount.values()) {
                ans += count * (count - 1);
            }
        }
        return ans;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)