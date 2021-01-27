# 之字形转换
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/zigzag-conversion/?utm_source=sc-github-wzz)
 ## 题目描述
 给定一个字符串 `s` 和一个整数 `numRows`. 你需要把 `s` 排布成一个 `numRows` 行的 "之" 字形. 然后返回逐行阅读的结果.

注意, "之" 字形是按照 下->右上->下->右上...的方向延伸的.

```
|   /|   /|
|  / |  / | ...
| /  | /  | ...
|/   |/   |/
```
 ### 样例说明
 **样例 1:**

```
输入: "PAYPALISHIRING", numRows = 3
输出: "PAHNAPLSIIGYIR"
解释: 
    转换之后我们会得到
    P   A   H   N
    A P L S I I G
    Y   I   R
    一行一行地读, 得到答案: "PAHNAPLSIIGYIR".
```

**样例 2:**

```
输入: "PAYPALISHIRING", numRows = 4
输出: "PINALSIGYAHRPI"
解释: 
    转换之后我们会得到
    P     I     N
    A   L S   I G
    Y A   H R
    P     I
    一行一行地读, 得到答案: "PINALSIGYAHRPI".
```

**样例 3:**

```
输入: "PAYPALISHIRING", numRows = 1
输出: "PAYPALISHIRING"
解释: 
    转换之后我们会得到
    PAYPALISHIRING
    一行一行地读, 得到答案: "PAYPALISHIRING".
```
 ### 参考代码
 The string "PAYPALISHIRING" is written in a zigzag pattern on a given number of rows like this: (you may want to display this pattern in a fixed font for better legibility)

P   A   H   N
A P L S I I G
Y   I   R
And then read line by line: "PAHNAPLSIIGYIR"
Write the code that will take a string and make this conversion given a number of rows:

string convert(string text, int nRows);
convert("PAYPALISHIRING", 3) should return "PAHNAPLSIIGYIR".
```java
public class Solution {
    public String convert(String s, int nRows) {
        int length = s.length();
        if (length <= nRows || nRows == 1) return s;
        char[] chars = new char[length];
        int step = 2 * (nRows - 1);
        int count = 0;
	    for (int i = 0; i < nRows; i++){
    		int interval = step - 2 * i;
    		for (int j = i; j < length; j += step){
    		   	chars[count] = s.charAt(j);
    			count++;
    			if (interval < step && interval > 0 
    && j + interval < length && count <  length){
    				chars[count] = s.charAt(j + interval);
    				count++;
    			}
    		}
    	}
        return new String(chars);
    }
}


```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)