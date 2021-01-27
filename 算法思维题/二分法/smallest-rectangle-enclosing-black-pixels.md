# 包裹黑色像素点的最小矩形
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/smallest-rectangle-enclosing-black-pixels/?utm_source=sc-github-wzz)
 ## 题目描述
 一个由二进制矩阵表示的图，`0` 表示白色像素点，`1` 表示黑色像素点。黑色像素点是联通的，即只有一块黑色区域。像素是水平和竖直连接的，给一个黑色像素点的坐标 `(x, y)` ，返回囊括所有黑色像素点的矩阵的最小面积。
 ### 样例说明
 **样例 1:**
```
输入：["0010","0110","0100"]，x=0，y=2
输出：6
解释：
矩阵左上角坐标是(0, 1), 右下角的坐标是(2, 2)
```

**样例 2:**
```
输入：["1110","1100","0000","0000"], x = 0, y = 1
输出：6
解释：
矩阵左上角坐标是(0,  0), 右下角坐标是(1, 3)
```
 ### 参考代码
 考点：
* 二分

题解：
根据题意，在列中需要找出第一个'1'出现的最左侧坐标和最右侧坐标，在行中需要找出第一个'1'出现的最上面坐标和最下面坐标。故采用二分的方法在区间查找即可。最后返回(right - left + 1) * (bottom - top + 1)即可。
```java
public class Solution {
    /**
     * @param image a binary matrix with '0' and '1'
     * @param x, y the location of one of the black pixels
     * @return an integer
     */
    public int minArea(char[][] image, int x, int y) {
        if (image == null || image.length == 0 || image[0].length == 0) {
            return 0;
        }
        
        int n = image.length;
        int m = image[0].length;
        
        int left = findLeft(image, 0, y);
        int right = findRight(image, y, m - 1);
        int top = findTop(image, 0, x);
        int bottom = findBottom(image, x, n - 1);

        return (right - left + 1) * (bottom - top + 1);
    }
    
    private int findLeft(char[][] image, int start, int end) {
        while (start + 1 < end) {
            int mid = start + (end - start) / 2;
            if (isEmptyColumn(image, mid)) {
                start = mid;
            } else {
                end = mid;
            }
        }
        
        if (isEmptyColumn(image, start)) {
            return end;
        }
        
        return start;
    }
    
    private int findRight(char[][] image, int start, int end) {
        while (start + 1 < end) {
            int mid = start + (end - start) / 2;
            if (isEmptyColumn(image, mid)) {
                end = mid;
            } else {
                start = mid;
            }
        }
        
        if (isEmptyColumn(image, end)) {
            return start;
        }
        
        return end;
    }
    
    private int findTop(char[][] image, int start, int end) {
        while (start + 1 < end) {
            int mid = start + (end - start) / 2;
            if (isEmptyRow(image, mid)) {
                start = mid;
            } else {
                end = mid;
            }
        }
        
        if (isEmptyRow(image, start)) {
            return end;
        }
        
        return start;
    }
    
    private int findBottom(char[][] image, int start, int end) {
        while (start + 1 < end) {
            int mid = start + (end - start) / 2;
            if (isEmptyRow(image, mid)) {
                end = mid;
            } else {
                start = mid;
            }
        }
        
        if (isEmptyRow(image, end)) {
            return start;
        }
        
        return end;
    }
    
    private boolean isEmptyColumn(char[][] image, int col) {
        for (int i = 0; i < image.length; i++) {
            if (image[i][col] == '1') {
                return false;
            }
        }
        return true;
    }
    
    private boolean isEmptyRow(char[][] image, int row) {
        for (int j = 0; j < image[0].length; j++) {
            if (image[row][j] == '1') {
                return false;
            }
        }
        return true;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)