# 整数转罗马数字
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/integer-to-roman/?utm_source=sc-github-wzz)
 ## 题目描述
 给定一个整数，将其转换成罗马数字。

保证给定的整数在`1`到`3999`的范围内。
 ### 样例说明
 **样例 1:**

```
输入: 1
输出: "I"
```

**样例 2:**

```
输入: 99
输出: "XCIX"
```
 ### 参考代码
 根据罗马数字的计数规则进行转换即可.
```java
public class Solution {
	public String intToRoman(int num) {
		if(num <= 0) {
			return "";
		}
	    int[] nums = {1000, 900, 500, 400, 100, 90, 50, 40, 10, 9, 5, 4, 1};
	    String[] symbols = {"M", "CM", "D", "CD", "C", "XC", "L", "XL", "X", "IX", "V", "IV", "I"};
	    StringBuilder res = new StringBuilder();
	    int digit=0;
	    while (num > 0) {
	        int times = num / nums[digit];
	        num -= nums[digit] * times;
	        for ( ; times > 0; times--) {
	            res.append(symbols[digit]);
	        }
	        digit++;
	    }
	    return res.toString();
	}
}

/////////////// version: 高频题班

public class Solution {
    /**
     * @param n The integer
     * @return Roman representation
     */
    public String intToRoman(int n) {
        String M[] = {"", "M", "MM", "MMM"};
        String C[] = {"", "C", "CC", "CCC", "CD", "D", "DC", "DCC", "DCCC", "CM"};
        String X[] = {"", "X", "XX", "XXX", "XL", "L", "LX", "LXX", "LXXX", "XC"};
        String I[] = {"", "I", "II", "III", "IV", "V", "VI", "VII", "VIII", "IX"};
        return M[n / 1000] + C[(n / 100) % 10] + X[(n / 10) % 10] + I[n % 10];
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)