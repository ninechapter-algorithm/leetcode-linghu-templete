# 转换字符串到整数（容易版）
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/string-to-integer/?utm_source=sc-github-wzz)
 ## 题目描述
 给一个字符串, 转换为整数. 你可以假设这个字符串是一个有效的整数的字符串形式， 且范围在32位整数之间 (-2<sup>31</sup> ~ 2<sup>31</sup> - 1)。
 ### 样例说明
 ```
样例  1:
	输入:  "123"
	输出: 123
	
	样例解释: 
	返回对应的数字.

样例 2:
	输入:  "-2"
	输出: -2
	
	样例解释: 
	返回对应的数字，注意负数.

```
 ### 参考代码
 要考虑给的字符串是否有符号。

然后从高位开始循环累加。
转换公示如下
字符串：$S_1S_2S_3S_4$ --> 数字：$((S_1*10+S_2)*10+S_3)*10+S_4$
```java
//version 1(use library function)
public class Solution {
    /**
     * @param str a string
     * @return an integer
     */
    public int stringToInteger(String str) {
        return Integer.valueOf(str);
    }
}

//version 2 
public class Solution {
    /**
     * @param str a string
     * @return an integer
     */
    public int stringToInteger(String str) {
        // Write your code here
        int integer = 0;
        int Minus = 0;
        
        if (str.charAt(0) == '-'){
            Minus = 1;
        }
        
        for (int i = Minus; i < str.length(); i++){
            integer = integer * 10 + str.charAt(i)-'0';
        }
        
        if (Minus == 1){
            integer = -integer;
        }
        return integer;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)