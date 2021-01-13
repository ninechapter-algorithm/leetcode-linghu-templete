# 快乐数
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/happy-number/?utm_source=sc-github-wzz)
 ## 题目描述
 写一个算法来判断一个数是不是"快乐数"。

一个数是不是快乐是这么定义的：对于一个正整数，每一次将该数替换为他每个位置上的数字的平方和，然后重复这个过程直到这个数变为1，或是无限循环但始终变不到1。如果可以变为1，那么这个数就是快乐数。
 ### 样例说明
 例1：
```
输入：19
输出：true
说明：

19是一个快乐的数字

     1 ^ 2 + 9 ^ 2 = 82
     8 ^ 2 + 2 ^ 2 = 68
     6 ^ 2 + 8 ^ 2 = 100
     1 ^ 2 + 0 ^ 2 + 0 ^ 2 = 1

```

例2：
```
输入：5
输出：false
说明：

5不是一个快乐的数字

25->29->85->89->145->42->20->4->16->37->58->89
再次出现89。
```
 ### 参考代码
 看看变化的过程中，是否出现重复，若出现，则代表不是快乐数
```java
public class Solution {
    private int getNextHappy(int n) {
        int sum = 0;
        while (n != 0) {
            sum += (n % 10) * (n % 10);
            n /= 10;
        }
        return sum;
    }
    
    public boolean isHappy(int n) {
        HashSet<Integer> hash = new HashSet<Integer>();
        while (n != 1) {
            if (hash.contains(n)) {
                return false;
            }
            hash.add(n);
            n = getNextHappy(n);
        }
        return true;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)