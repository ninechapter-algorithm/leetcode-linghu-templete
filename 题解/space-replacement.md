# 空格替换
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/space-replacement/?utm_source=sc-github-wzz)
 ## 题目描述
 设计一种方法，将一个字符串中的所有空格替换成 `%20` 。你可以假设该字符串有足够的空间来加入新的字符，且你得到的是“真实的”字符长度。

你的程序还需要返回被替换后的字符串的长度。
 ### 样例说明
 **样例 1：**
```
输入：string[] = "Mr John Smith" and length = 13
输出：string[] = "Mr%20John%20Smith" and return 17
解释：
对于字符串 "Mr John Smith"，长度为 13。替换空格之后，参数中的字符串需要变为 "Mr%20John%20Smith"，并且把新长度 17 作为结果返回。
```
**样例 2：**
```
输入：string[] = "LintCode and Jiuzhang" and length = 21
输出：string[] = "LintCode%20and%20Jiuzhang" and return 25
解释：
对于字符串 "LintCode and Jiuzhang"，长度为 21。替换空格之后，参数中的字符串需要变为 "LintCode%20and%20Jiuzhang"，并且把新长度 25 作为结果返回。
```
 ### 参考代码
 ```java
public class Solution {
    /*
     * @param string: An array of Char
     * @param length: The true length of the string
     * @return: The true length of new string
     */
    public int replaceBlank(char[] string, int length) {
        // write your code here
        if(0==length) return 0;
        int num = 0;
        for(int i=0;i<length;i++){
            if(string[i] == ' ') num++;
        }
        
        int newLen = length + num*2;
        string[newLen] = 0;
        int j = 1;
        for(int i=length-1;i>=0;i--){
            if(string[i] != ' '){
                string[newLen - j] = string[i];
                j++;
            }
            else{
                string[newLen - j] = '0';
                j++;
                string[newLen - j] = '2';
                j++;
                string[newLen - j] = '%';
                j++; 
            }
        }
        return newLen;
    }
};
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)