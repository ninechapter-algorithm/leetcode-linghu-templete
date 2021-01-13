# 跳跃游戏
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/jump-game/?utm_source=sc-github-wzz)
 ## 题目描述
 <p>给出一个非负整数数组，你最初定位在数组的第一个位置。　　　</p><p>数组中的每个元素代表你在那个位置可以跳跃的最大长度。　　　　</p><p>判断你是否能到达数组的最后一个位置。</p>
 ### 样例说明
 ***样例 1***
```
输入 : [2,3,1,1,4]
输出 : true
```

***样例 2***
```
输入 : [3,2,1,0,4]
输出 : false
```
 ### 参考代码
 Given an array of non-negative integers, you are initially positioned at the first index of the array.

Each element in the array represents your maximum jump length at that position.

Determine if you are able to reach the last index.

For example:
A = [2,3,1,1,4], return true.

A = [3,2,1,0,4], return false.

```
[[java]]
// version 1: Dynamic Programming
// 这个方法，复杂度是 O(n^2) 可能会超时，但是依然需要掌握。
public class Solution {
    public boolean canJump(int[] A) {
        boolean[] can = new boolean[A.length];
        can[0] = true;
        
        for (int i = 1; i < A.length; i++) {
            for (int j = 0; j < i; j++) {
                if (can[j] && j + A[j] >= i) {
                    can[i] = true;
                    break;
                }
            }
        }
        
        return can[A.length - 1];
    }
}


// version 2: Greedy
public class Solution {
    public boolean canJump(int[] A) {
        // think it as merging n intervals
        if (A == null || A.length == 0) {
            return false;
        }
        int farthest = A[0];
        for (int i = 1; i < A.length; i++) {
            if (i <= farthest && A[i] + i >= farthest) {
                farthest = A[i] + i;
            }
        }
        return farthest >= A.length - 1;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)