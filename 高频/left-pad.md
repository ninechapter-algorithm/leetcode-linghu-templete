# 左填充
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/left-pad/?utm_source=sc-github-wzz)
 ## 题目描述
 实现一个leftpad库，如果不知道什么是leftpad可以看样例
 ### 样例说明
 例1:
```
输入:
leftpad("foo", 5)
输出:
"  foo"
```
例2:
```
输入:
leftpad("foobar", 6)
输出:
"foobar"
```
例3:
```
输入:
leftpad("1", 2, "0")
输出:
"01"
```

 ### 参考代码
 按要求填充即可
```java
public class StringUtils {
    /**
     * @param originalStr the string we want to append to with spaces
     * @param size the target length of the string
     * @return a string
     */
    static public String leftPad(String originalStr, int size) {
        // Write your code here
        return leftPad(originalStr, size, ' ');
    }

    /**
     * @param originalStr the string we want to append to
     * @param size the target length of the string
     * @param padChar the character to pad to the left side of the string
     * @return a string
     */
    static public String leftPad(String originalStr, int size, char padChar) {
        // Write your code here
        StringBuffer sb = new StringBuffer();
        for (int i = 0; i < size - originalStr.length(); ++i)
            sb.append(padChar);
        sb.append(originalStr);
        return sb.toString();
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)