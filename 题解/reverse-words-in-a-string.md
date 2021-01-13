# 翻转字符串中的单词
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/reverse-words-in-a-string/?utm_source=sc-github-wzz)
 ## 题目描述
 <span style="line-height: 1.42857143;">给定一个字符串，逐个翻转字符串中的每个单词。</span>
 ### 样例说明
 ```
样例  1:
	输入:  "the sky is blue"
	输出:  "blue is sky the"
	
	样例解释: 
	返回逐字反转的字符串.

样例 2:
	输入:  "hello world"
	输出:  "world hello"
	
	样例解释: 
	返回逐字反转的字符串.

```
 ### 参考代码
 Given an input string, reverse the string word by word.

For example,
Given s = "the sky is blue",
return "blue is sky the".
```java
public class Solution {
    /*
     * @param s: A string
     * @return: A string
     */
    public String reverseWords(String s) {
        // write your code here
        if(s.length() == 0 || s == null){
            return " ";
        }
        //按照空格将s切分
        String[] array = s.split(" ");
        StringBuilder sb = new StringBuilder();
    	//从后往前遍历array，在sb中插入单词
        for(int i = array.length - 1; i >= 0; i--){
            if(!array[i].equals("")) {
                if (sb.length() > 0) {
                    sb.append(" ");
                }
                
                sb.append(array[i]);
            }
        }
        return sb.toString();
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)