# 字符转整数
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/char-to-integer/?utm_source=sc-github-wzz)
 ## 题目描述
 将字符转换为一个整数。你可以假设字符是ASCII码，也就是说转换后的整数在0~255之间。
 ### 样例说明
 ```
样例  1:
	输入:  'a'
	输出: 97
	
	样例解释: 
	返回ASCII码中对应的数字.

样例 2:
	输入:  '%'
	输出: 37
	
	样例解释: 
	返回ASCII码中对应的数字.

```
 ### 参考代码
 类型转换
```java
public class Solution {
    /**
     * @param character a character
     * @return an integer
     */
    public int charToInteger(char character) {
        return (int) character;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)