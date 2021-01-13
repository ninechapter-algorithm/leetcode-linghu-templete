# 螺旋矩阵 II
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/spiral-matrix-ii/?utm_source=sc-github-wzz)
 ## 题目描述
 给定一个数n, 生成一个包含1~$n^2$的螺旋形矩阵. 

(螺旋由外向内顺时针旋转, 可参照样例)
 ### 样例说明
 **样例 1:**

```
输入: 2
输出:
[
  [1, 2],
  [4, 3]
]
```

**样例 2:**
```
输入: 3
输出:
[
  [ 1, 2, 3 ],
  [ 8, 9, 4 ],
  [ 7, 6, 5 ]
]
```
 ### 参考代码
 **方法1:**

模拟螺旋形, 依次填入.

定义x, y为当前应填入数字的位置, d标志该位置前进的方向.

初始x, y在左上角, 即第一个位置, d标志右方.

每填入一个数字, 根据方向移动(x, y), 如果移动后的位置超过了边界或者已经被填过, 则转弯.

d转弯的顺序依次是: 右下左上. 直到填入了n\*n个数字为止即可.

**方法2:**

填数过程同上, 而写法不同, 类似"循环展开"的优化, 速度更快.

Java实现只提供了方法2, 方法1的实现参考C++
```java
public class Solution {
    public int[][] generateMatrix(int n) {
        if (n < 0) {
            return null;
        }

        int[][] result = new int[n][n];

        int xStart = 0;
        int yStart = 0;
        int num = 1;

        while (n > 0) {
            if (n == 1) {
                result[yStart][xStart] = num++;
                break;
            }

            for (int i = 0; i < n - 1; i++) {
                result[yStart][xStart + i] = num++;
            }

            for (int i = 0; i < n - 1; i++) {
                result[yStart + i][xStart + n - 1] = num++;
            }

            for (int i = 0; i < n - 1; i++) {
                result[yStart + n - 1][xStart + n - 1 - i] = num++;
            }

            for (int i = 0; i < n - 1; i++) {
                result[yStart + n - 1 - i][xStart] = num++;
            }

            xStart++;
            yStart++;
            n = n - 2;
        }

        return result;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)