# 	
地下城游戏
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/dungeon-game/?utm_source=sc-github-wzz)
 ## 题目描述
 恶魔抓住了公主（P）并将她关在地牢的右下角。地牢由M x N的2D网格房间组成，。我们英勇的骑士（K）最初位于左上角的房间，必须通过地牢的房间来拯救公主。

骑士的初始生命值由正整数表示。如果他的生命值在任何时候下降到0或更低，他会立即死亡。

有些房间是由恶魔守卫的，因此骑士进入这些房间时会失去生命值（负整数）；其他房间要么是空的（0），要么包含增加骑士健康的魔法球（正整数）。

为了尽快到达公主所在的地方，骑士决定在每一步中仅向右或向下移动。

编写一个函数来确定骑士的最少的初始生命值，使得他能够拯救公主。

例如，给定下面的地下城，如果骑士遵循最佳路径 右-> 右 -> 下 -> 下，则骑士的初始生命值必须至少为7。

```plain
| -2(K)   | -3     | 3        |
| -5      | -10    | 1        |
| 10      | 30     | -5(P)    |
```
 ### 样例说明
 **样例1**

```plain
输入: [[-2,-3,3],[-5,-10,1],[10,30,-5]]
输出: 7
说明:
路径 右右下下 是最优解
```

**样例2**

```plain
输入: [[-2,0,3],[-5,100,-999],[10,30,-5]]
输出: 3
说明:
路径 右下下右 是最优解
```


 ### 参考代码
 本题采用二分+dp check的做法
- 二分是对于答案进行二分。
- check的时候我们要用dp进行，考虑到起点用mid的血量开始到终点是否够，最后比较得出答案
```java
public class Solution {
  private boolean canSurvive(int health, int[][] dungeon) {
    int n = dungeon.length, m = dungeon[0].length;
    int[][] f = new int[n][m];

    f[0][0] = dungeon[0][0] + health;
    if (f[0][0] <= 0) {
      return false;
    }
    
    for (int i = 1; i < n; i++) {
      f[i][0] = f[i - 1][0] == Integer.MIN_VALUE
                ? Integer.MIN_VALUE
                : f[i - 1][0] + dungeon[i][0];
      if (f[i][0] <= 0) {
        f[i][0] = Integer.MIN_VALUE;
      }
    }
    for (int i = 1; i < m; i++) {
      f[0][i] = f[0][i - 1] == Integer.MIN_VALUE
                ? Integer.MIN_VALUE
                : f[0][i - 1] + dungeon[0][i];
      if (f[0][i] <= 0) {
        f[0][i] = Integer.MIN_VALUE;
      }
    }
    
    for (int i = 1; i < n; i++) {
      for (int j = 1; j < m; j++) {
        f[i][j] = Math.max(f[i - 1][j], f[i][j - 1]);
        if (f[i][j] == Integer.MIN_VALUE) {
          continue;
        }
        f[i][j] += dungeon[i][j];
        if (f[i][j] <= 0) {
          f[i][j] = Integer.MIN_VALUE;
        }
      }
    }
    
    return f[n - 1][m - 1] > 0;
  }
  
  public int calculateMinimumHP(int[][] dungeon) {
    int start = 1, end = Integer.MAX_VALUE - 1;
    while (start + 1 < end) {
      int mid = (end - start) / 2 + start;
      if (canSurvive(mid, dungeon)) {
        end = mid;
      } else {
        start = mid;
      }
    }
    if (canSurvive(start, dungeon)) {
      return start;
    }
    return end;
  }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)