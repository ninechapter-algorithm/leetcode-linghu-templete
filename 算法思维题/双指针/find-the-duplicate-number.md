# 寻找重复的数
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/find-the-duplicate-number/?utm_source=sc-github-wzz)
 ## 题目描述
 给出一个数组 `nums` 包含 `n + 1` 个整数，每个整数是从 `1` 到 `n` (包括边界)，保证至少存在一个重复的整数。假设只有一个重复的整数，找出这个重复的数。
 ### 样例说明
 **样例 1:**
```
输入:
[5,5,4,3,2,1]
输出:
5
```

**样例 2:**
```
输入:
[5,4,4,3,2,1]
输出:
4
```
 ### 参考代码
 九章算法强化班中讲过的基于值的二分法。
这个题比较好的理解方法是画一个坐标轴：

- x轴是 0, 1, 2, ... n。
- y轴是对应的 <=x 的数的个数，比如 <=0 的数的个数是0，就在（0,0）这个坐标画一个点。<=n 的数的个数是 n+1 个，就在 (n,n+1)画一个点。

把所有的点连接起来之后，是一个类似下图的折线：

![图片](https://media-cdn.jiuzhang.com/markdown/images/8/13/f2b4a1d0-9ecb-11e8-b810-0242ac110002.jpg)

我们可以知道这个折线图的有如下的一些属性：

1. 大部分时候，我们会沿着斜率为 1 的那条虚线前进
2. 如果出现了一些空缺的数，就会有横向的折线
3. 一旦出现了重复的数，就会出现一段斜率超过 1 的折线
4. 斜率超过 1 的折线只会出现一次

试想一下，对比 y=x 这条虚线，当折线冒过了这条虚线出现在这条虚线的上方的时候，一定是遇到了一个重复的数。
一旦越过了这条虚线以后，就再也不会掉到虚线的下方或者和虚线重叠。
因为折线最终会停在 (n,n+1) 这个位置，如果要从 y=x 这条虚线或者这条虚线的下方到达 (n,n+1) 这个位置，
一定需要一个斜率 > 1的折线段，而这个与题目所说的重复的数只有一个就是矛盾的。因此可以证明，斜率超过1 的折线只会出现1次，
且会将折线整体带上 y=x 这条虚线的上方。因此第一个在 y=x 上方的 x 点，就是我们要找的重复的数。

时间复杂度是 $O(nlogn)$
```java
public class Solution {
    /**
     * @param nums an array containing n + 1 integers which is between 1 and n
     * @return the duplicate one
     */
    public int findDuplicate(int[] nums) {
        // Write your code here
        int l = 1;
        int r = nums.length - 1;  // n
        
        while (l + 1 < r) {
            int mid = l + (r - l) / 2;
            if (count(nums, mid) <= mid) {
                l = mid;
            } else {
                r = mid;
            }
        }
        
        if (count(nums, l) <= l) {
            return r;
        }
        return l;
    }
    
    private int count(int[] nums, int mid) {
        int cnt = 0;
        for (int item : nums) {
            if (item <= mid) {
                cnt++;
            }
        }
        return cnt;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)