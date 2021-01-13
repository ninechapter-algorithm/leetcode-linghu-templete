# 能否放置花
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/can-place-flowers/?utm_source=sc-github-wzz)
 ## 题目描述
 假设你有一个长花圃，其中有些地块已经被种植了，但是有些地块没有。但是，花不能够在相邻的地块下种植 - 他们会争夺水从而导致两者的死亡。

给定一个花圃（用一个包含0和1的数组来表示，其中0代表空，1代表非空），和一个数字**n**，返回n朵新的花在这个花圃上以能否在不违反“无相邻花”的规则种植。
 ### 样例说明
 **样例1**
```
输入: flowerbed = [1,0,0,0,1], n = 1
输出: True
```
**样例2**
```
输入: flowerbed = [1,0,0,0,1], n = 2
输出: False
```
 ### 参考代码
 比较基础的模拟题，按照题目要求从头开始模拟种植即可。
```java
public class Solution {
    public boolean canPlaceFlowers(int[] flowerbed, int n) {
        int count = 0;
        for (int i = 0; i < flowerbed.length; i++) {
            if (flowerbed[i] == 0 && (i == 0 || flowerbed[i - 1] == 0)
            && (i == flowerbed.length - 1 || flowerbed[i + 1] == 0)) {
                flowerbed[i] = 1;
                count++;
            }
            if (count >= n) {
                return true;
            }
        }
        return false;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)