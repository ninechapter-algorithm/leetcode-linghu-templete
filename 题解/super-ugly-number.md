# 超级丑数
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/super-ugly-number/?utm_source=sc-github-wzz)
 ## 题目描述
 写一个程序来找第 *n* 个超级丑数。

超级丑数是所有的质数因子都在给定的的质数集合内的正整数。

比如给定质数集合 `[2, 7, 13, 19]`, 那么 `[1, 2, 4, 7, 8, 13, 14, 16, 19, 26, 28, 32]` 是前 12 个超级丑数。
 ### 样例说明
 **样例 1:**

```
输入: n = 6, [2,7,13,19]
输出: 13
```

**样例 2:**

```
输入: n = 11, [2,3,5]
输出: 15
```
 ### 参考代码
 **做法1**:

使用小根堆, 初始将1放入堆, 循环 n-1 次, 每次取出堆顶, 然后将该值与素数列表每个数的乘积再次放入堆.

注意可能会有数重复入堆, 所以还需要额外的数据结构记录一个数是否出现过, 把重复的数排除, 以保证取出的堆顶是从小到大的超级丑数.

n-1 次循环之后, 此时的堆顶即是第 n 个丑数.

时间复杂度 O(nklogn)

**做法2**:

依次求出前n个超级丑数. 定义times[i]表示当前的超级丑数的质因数中, 列表中第i个素数的次数. uglys[i]表示第i+1个素数.

初始 times[i] = 0, uglys[0] = 1, 然后依次由 uglys[0] ~ uglys[i] 求出 uglys[i+1]:

1. 枚举, 求出 uglys[times[j]] * prime[j] 的最小值, 即是 uglys[i+1]
2. 更新对应的 times[j], 即 若 uglys[times[j]] * prime[j] == uglys[i+1], times[j]++

时间复杂度 O(nk)

可参考 <https://blog.csdn.net/happyaaaaaaaaaaa/article/details/50850473>
```java
public class Solution {
    /**
     * @param n a positive integer
     * @param primes the given prime list
     * @return the nth super ugly number
     */
    public int nthSuperUglyNumber(int n, int[] primes) {
        int[] times = new int[primes.length];
        int[] uglys = new int[n];
        uglys[0] = 1;

        for (int i = 1; i < n; i++) {
            uglys[i] = Integer.MAX_VALUE;
            for (int j = 0; j < primes.length; j++) {
                uglys[i] = Math.min(uglys[i], primes[j] * uglys[times[j]]);
            }

            for (int j = 0; j < times.length; j++) {
                if (uglys[times[j]] * primes[j] == uglys[i]) {
                    times[j]++;
                }
            }
        }
        return uglys[n - 1];
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)