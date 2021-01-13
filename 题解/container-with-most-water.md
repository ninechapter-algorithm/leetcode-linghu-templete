# 装最多水的容器
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/container-with-most-water/?utm_source=sc-github-wzz)
 ## 题目描述
 给定 *n* 个非负整数 a<sub>1</sub>, a<sub>2</sub>, ..., a<sub>n</sub>, 每个数代表了坐标中的一个点 `(i, ai)`。画 *n* 条垂直线，使得 *i* 垂直线的两个端点分别为`(i, ai)`和`(i, 0)`。找到两条线，使得其与 *x* 轴共同构成一个容器，以容纳最多水。

 ### 样例说明
 **样例 1:**

```
输入: [1, 3, 2]
输出: 2
解释:
选择 a1, a2, 容量为 1 * 1 = 1
选择 a1, a3, 容量为 1 * 2 = 2
选择 a2, a3, 容量为 2 * 1 = 2
```

**样例 2:**

```
输入: [1, 3, 2, 2]
输出: 4
解释:
选择 a1, a2, 容量为 1 * 1 = 1
选择 a1, a3, 容量为 1 * 2 = 2
选择 a1, a4, 容量为 1 * 3 = 3
选择 a2, a3, 容量为 2 * 1 = 2
选择 a2, a4, 容量为 2 * 2 = 4
选择 a3, a4, 容量为 2 * 1 = 2
```

 ### 参考代码
 题意: 给定一个非负整数数组, 选取i, j使得 $|i-j| \times min(a[i], a[j])| 最大

设定两个指针, 初始在两端, 计算这两个组成的容量, 然后移动值较小的那个, 所有计算结果取最大.

可以反证法证明这样可以得到最优答案
```java
public class Solution {
    /**
     * @param heights: an array of integers
     * @return: an integer
     */
    int computeArea(int left, int right,  int[] heights) {
        return (right-left)*Math.min(heights[left], heights[right]);
    }
    
    public int maxArea(int[] heights) {
        // write your code here
        int left = 0, ans=  0 ; 
        int right = heights.length - 1;
        while (left <= right) {
            ans = Math.max(ans,computeArea(left, right, heights));
            if (heights[left]<=heights[right])
                left++;
            else
                right--;
        }
        return ans;
    }
}

--------------------------------------


public class Solution {
    // for any i, the maxium area will be the farthest j that has a[j] > a[i];
    public int maxArea(int[] height) {
        if (height == null || height.length < 2) {
            return 0;
        }
        int max = 0;
        int left = 0;
        int right = height.length -1;
        while (left < right) {
            max = Math.max( max, (right - left) * Math.min(height[left], height[right]));
            if (height[left] < height[right]){
                left++;
            } else {
                right--;
            }
        }
        return max;
        
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)