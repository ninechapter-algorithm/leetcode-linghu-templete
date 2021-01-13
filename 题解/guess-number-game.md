# 猜数游戏
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/guess-number-game/?utm_source=sc-github-wzz)
 ## 题目描述
 我们正在玩猜数游戏。 游戏如下：
我从 **1** 到 **n** 选择一个数字。 你需要猜我选择了哪个号码。
每次你猜错了，我会告诉你这个数字与你猜测的数字相比是大还是小。
你调用一个预定义的接口 `guess(int num)`，它会返回 3 个可能的结果(-1，1或0):
-1代表这个数字小于你猜测的数
1代表这个数字大于你猜测的数
0代表这个数字等于你猜测的数
 ### 样例说明
 
 ### 参考代码
 ```java
// version: 高频题班

/* The guess API is defined in the parent class GuessGame.
   @param num, your guess
   @return -1 if my number is lower, 1 if my number is higher, otherwise return 0
      int guess(int num); */

public class Solution extends GuessGame {
    /**
     * @param n an integer
     * @return the number you guess
     */
    public int guessNumber(int n) {
        // Write your code here
        int l = 1, r = n;
        while (l <= r) {
            int mid = l + (r - l) / 2;
            int res = guess(mid);
            if (res == 0) {
                return mid;
            }
            
            if (res == -1) {
                r = mid - 1;
            } else {
                l = mid + 1;
            }
        }
        return -1;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)