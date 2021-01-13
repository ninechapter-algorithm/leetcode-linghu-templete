# 接雨水
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/trapping-rain-water/?utm_source=sc-github-wzz)
 ## 题目描述
 给出 *n* 个非负整数，代表一张X轴上每个区域宽度为 `1` 的海拔图, 计算这个海拔图最多能接住多少（面积）雨水。

![Trapping Rain Water](https://lintcode-media.s3.amazonaws.com/problem/rainwatertrap.png "Trapping Rain Water I")
 ### 样例说明
 **样例 1:**
```
输入: [0,1,0]
输出: 0
```

**样例 2:**
```
输入: [0,1,0,2,1,0,1,3,2,1,2,1]
输出: 6
```
 ### 参考代码
 每个位置上的盛水数目 = `min(左侧最高，右侧最高) - 当前高度`

从左到右扫描一边数组，获得每个位置往左这一段的最大值，再从右到左扫描一次获得每个位置向右的最大值。
然后最后再扫描一次数组，计算每个位置上的盛水数目。

时间复杂度 $O(n)$，空间复杂度 $O(n)$
```python
class Solution:
    """
    @param heights: a list of integers
    @return: a integer
    """
    def trapRainWater(self, heights):
        if not heights:
            return 0
            
        left_max = []
        curt_max = -sys.maxsize
        for height in heights:
            curt_max = max(curt_max, height)
            left_max.append(curt_max)
            
        right_max = []
        curt_max = -sys.maxsize
        for height in reversed(heights):
            curt_max = max(curt_max, height)
            right_max.append(curt_max)
            
        right_max = right_max[::-1]
            
        water = 0
        n = len(heights)
        for i in range(n):
            water += (min(left_max[i], right_max[i]) - heights[i])
        return water
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)