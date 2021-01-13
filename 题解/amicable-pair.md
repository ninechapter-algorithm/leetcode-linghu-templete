# 相亲数
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/amicable-pair/?utm_source=sc-github-wzz)
 ## 题目描述
 一对整数是相亲数是说他们各自的所有有效因子（除了自己以外的因子）之和等于另外一个数。比如 (220, 284) 就是一对相亲数。因为：

* 220的所有因子：1+2+4+5+10+11+20+22+44+55+110 = 284
* 284的所有因子：1+2+4+71+142 = 220 

给出整数 k，求 1~k 之间的所有相亲数对。
 ### 样例说明
 **样例 1：**
```
输入：300
输出：[[220,284]]
```
**样例 2：**
```
输入：220
输出：[]
```
 ### 参考代码
 ```java
public class Solution {
    /**
     * @param k an integer
     * @return all amicable pairs
     */
    public int factorSum(int n) {
        int sum = 1, i;
        for (i = 2; i * i < n; ++i) {
            if (n % i == 0) {
                sum += i + n / i;
            }
        }
        if (i * i == n) {
            sum += i;
        }
        return sum;
    }
    
    public List<List<Integer>> amicablePair(int k) {
        List<List<Integer>> result = new ArrayList<List<Integer>>();
        for (int i = 2; i <= k; ++i) {
            int amicable = factorSum(i);
            if (amicable <= i || amicable > k) {
                continue;
            }
            if (factorSum(amicable) == i) {
                ArrayList<Integer> pair = new ArrayList<Integer>();
                pair.add(i);
                pair.add(amicable);
                result.add(pair);
            }
        }
        return result;
    }
}

```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)