# 旋转字符串
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/rotate-string/?utm_source=sc-github-wzz)
 ## 题目描述
 给定一个字符串（以字符数组的形式给出）和一个偏移量，根据偏移量`原地`旋转字符串(从左向右旋转)。
 ### 样例说明
 **样例  1:**

```
输入:  str="abcdefg", offset = 3
输出:  str = "efgabcd"	
样例解释:  注意是原地旋转，即str旋转后为"efgabcd"
```

**样例 2:**

```
输入: str="abcdefg", offset = 0
输出: str = "abcdefg"	
样例解释: 注意是原地旋转，即str旋转后为"abcdefg"
```


**样例 3:**

```
输入: str="abcdefg", offset = 1
输出: str = "gabcdef"	
样例解释: 注意是原地旋转，即str旋转后为"gabcdef"
```

**样例 4:**

```
输入: str="abcdefg", offset =2
输出: str = "fgabcde"	
样例解释: 注意是原地旋转，即str旋转后为"fgabcde"
```

**样例 5:**

```
输入: str="abcdefg", offset = 10
输出: str = "efgabcd"	
样例解释: 注意是原地旋转，即str旋转后为"efgabcd"
```

 ### 参考代码
 通过将原本的字符串倒置，可以将后面的旋转到前面。
但是结果两段分别倒置了，再分别将两段倒置回来即可。

时间复杂度O(n)
```java
public class Solution {
    /**
     * @param str: an array of char
     * @param offset: an integer
     * @return: nothing
     */
    public void rotateString(char[] str, int offset) {
        // write your code here
        if (str == null || str.length == 0)
            return;
            
        offset = offset % str.length;
        reverse(str, 0, str.length - offset - 1);
        reverse(str, str.length - offset, str.length - 1);
        reverse(str, 0, str.length - 1);
    }
    
    private void reverse(char[] str, int start, int end) {
        for (int i = start, j = end; i < j; i++, j--) {
            char temp = str[i];
            str[i] = str[j];
            str[j] = temp;
        }
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)