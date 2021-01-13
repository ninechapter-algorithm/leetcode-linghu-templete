# 跳跃游戏 II
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/jump-game-ii/?utm_source=sc-github-wzz)
 ## 题目描述
 <p>给出一个非负整数数组，你最初定位在数组的第一个位置。<br></p><p><span style="line-height: 1.42857143;">数组中的每个元素代表你在那个位置可以跳跃的最大长度。</span>　　　</p><p>你的目标是使用最少的跳跃次数到达数组的最后一个位置。</p>
 ### 样例说明
 ***样例 1***
```
输入 : [2,3,1,1,4]
输出 : 2
解释 : 到达最后位置的最小跳跃次数是2(从下标0到1跳跃1个距离长度，然后跳跃3个距离长度到最后位置)
```
 ### 参考代码
 Given an array of non-negative integers, you are initially positioned at the first index of the array.

Each element in the array represents your maximum jump length at that position.

Your goal is to reach the last index in the minimum number of jumps.

For example:
Given array A = [2,3,1,1,4]

The minimum number of jumps to reach the last index is 2. (Jump 1 step from index 0 to 1, then 3 steps to the last index.)<div><br></div><div>更优化详细题解请至九章微博：<a href="http://weibo.com/3948019741/BFp8AtIKi" target="_blank">http://weibo.com/3948019741/BFp8AtIKi</a></div>
```java
// version 1: Dynamic Programming
// 这个方法，复杂度是 O(n^2)，会超时，但是依然需要掌握。
public class Solution {
    public int jump(int[] A) {
        // state
        int[] steps = new int[A.length];

        // initialize
        steps[0] = 0;
        for (int i = 1; i < A.length; i++) {
            steps[i] = Integer.MAX_VALUE;
        }

        // function
        for (int i = 1; i < A.length; i++) {
            for (int j = 0; j < i; j++) {
                if (steps[j] != Integer.MAX_VALUE && j + A[j] >= i) {
                    steps[i] = Math.min(steps[i], steps[j] + 1);
                }
            }
        }
        
        // answer
        return steps[A.length - 1];
    }
}


// version 2: Greedy
public class Solution {
    public int jump(int[] A) {
        if (A == null || A.length == 0) {
            return -1;
        }
        int start = 0, end = 0, jumps = 0;
        while (end < A.length - 1) {
            jumps++;
            int farthest = end;
            for (int i = start; i <= end; i++) {
                if (A[i] + i > farthest) {
                    farthest = A[i] + i;
                }
            }
            start = end + 1;
            end = farthest;
        }
        return jumps;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)