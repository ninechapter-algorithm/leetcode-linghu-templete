# 各位相加
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/add-digits/?utm_source=sc-github-wzz)
 ## 题目描述
 给出一个非负整数 `num`，反复的将所有位上的数字相加，直到得到一个一位的整数。
 ### 样例说明
 例1:
```
输入:
num=38
输出:
2
解释:
过程如下： 3 + 8 = 11, 1 + 1 = 2. 因为 2 只有一个数字，返回 2.

```

例2:
```
输入:
num=9
输出:
9
解释:
9<10,返回 9.
```

 ### 参考代码
 反复相加，直到最后小于10,退出循环
```java
#### 参考程序 - Java



	public class Solution {

		public int addDigits(int num) {

			if (num == 0) {

			    return 0;

			}

			int ans = 0;

			for (; num != 0; ) {

			    int digit = num % 10;

			    ans = (ans * 10 + digit) % 9;

			    num /= 10;

			}

			return ans == 0 ? 9 : ans;

		}

	}

// 九章硅谷求职算法集训营版本
public class Solution {
    /**
     * @param num: a non-negative integer
     * @return: one digit
     */
    public int addDigits(int num) {
        while (num >= 10) {
            int sum = 0;
            while (num > 0) {
                sum += num % 10;
                num /= 10;
            }
            
            num = sum;
        }
        
        return num;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)