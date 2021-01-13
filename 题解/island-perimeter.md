# 岛的周长
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/island-perimeter/?utm_source=sc-github-wzz)
 ## 题目描述
 给定一张用二维数组表示的网格地图，其中1表示陆地单元格，0表示水域单元格。网格地图中的单元格视为水平/垂直相连（斜向不相连）。这个网格地图四周完全被水域包围着，并且其中有且仅有一个**岛**（定义为一块或多块相连的陆地单元格）。这个岛不包含**湖**（定义为不和外围水域相连的水域单元格）。一个地图单元格是边长为1的一个正方形；网格地图是一个矩形，并且它的长和宽不超过100。你要做的是求出这个岛的周长。
 ### 样例说明
 ```
[[0,1,0,0],
 [1,1,1,0],
 [0,1,0,0],
 [1,1,0,0]]

答案：16
```
说明：岛的边界为下图中被标为黄色的边，其周长即为16：
![](https://lintcode-media.s3.amazonaws.com/problem/island.png "")
 ### 参考代码
 对于一片陆地，
* 若其上方没有陆地，则贡献一条边；
* 若其左方没有陆地，则贡献一条边；
* 若其下方没有陆地，则贡献一条边；
* 若其右方没有陆地，则贡献一条边；

遍历所有陆地求出所有贡献和即可。
```java
public class Solution {
    int []dx  = {1, 0, -1, 0};
    int []dy  = {0, 1, 0, -1};
    
    private boolean valid(int x, int y, int[][] grid) {
        if (0 <= x && x < grid.length && 0 <= y && y < grid[x].length) {
            return grid[x][y] == 0;
        }
        return true;
    } 
    public int islandPerimeter(int[][] grid) {
        int Perimeter = 0;
        
        for(int i = 0; i < grid.length; i ++) {
            for(int j = 0; j < grid[i].length;j ++) {
                if(grid[i][j] == 1) {
                    for (int k = 0; k < 4; k++) {
                        if (valid(i + dx[k], j + dy[k], grid)) {
                            Perimeter ++;
                        }
                    }
                }
            }
        }
        return Perimeter;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)