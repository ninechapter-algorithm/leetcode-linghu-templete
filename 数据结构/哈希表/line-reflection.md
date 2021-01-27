# 直线对称
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/line-reflection/?utm_source=sc-github-wzz)
 ## 题目描述
 给定二维平面上的`n`点，请问是否有这样一条与y轴平行的线使所有点对称。
 ### 样例说明
 **样例1**

```
输入: [[1,1],[-1,1]]
输出: true
```

**样例2**

```
输入: [[1,1],[-1,-1]]
输出: false
```
 ### 参考代码
 ```java
public class Solution {
    public boolean isReflected(int[][] points) {
        int max = 0, min = 0;
        HashMap<Integer, HashSet<Integer>> hashmap = new HashMap<>();
        for (int i = 0; i < points.length; i++) {
            max = Math.max(points[i][0], max);
            min = Math.min(points[i][0], min);
            if (!hashmap.containsKey(points[i][1])) {
                HashSet<Integer> hashset = new HashSet<>();
                hashset.add(points[i][0]);
                hashmap.put(points[i][1], hashset);
            } else {
                hashmap.get(points[i][1]).add(points[i][0]);
            }
        }
        for (int i = 0; i < points.length; i++) {
            if (!hashmap.containsKey(points[i][1]) || !hashmap.get(points[i][1]).contains(max + min - points[i][0])) {
                return false;
            }
        }
        return true;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)