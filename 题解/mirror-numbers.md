# 镜像数字
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/mirror-numbers/?utm_source=sc-github-wzz)
 ## 题目描述
 一个镜像数字是指一个数字旋转180度以后和原来一样(倒着看)。例如，数字"69"，"88"，和"818"都是镜像数字。
写下一个函数来判断是否这个数字是镜像的。数字用字符串来表示。
 ### 样例说明
 
 ### 参考代码
 将倒过来能看成数字的数字哈希一下，就能进行转换判断了。
```java
public class Solution {
    /**
     * @param num a string
     * @return true if a number is strobogrammatic or false
     */
    public boolean isStrobogrammatic(String num) {
        // Write your code here
        Map<Character, Character> map = new HashMap<Character, Character>();
        map.put('6', '9');
        map.put('9', '6');
        map.put('0', '0');
        map.put('1', '1');
        map.put('8', '8');
        int left = 0, right = num.length() - 1;
        while (left <= right) {
            if (!map.containsKey(num.charAt(left))) {
                return false;
            }
            if (map.get(num.charAt(left)) != num.charAt(right)) {
                return false;
            }
            left ++;
            right --;
        }
        return true;
    }
}

// version: 高频题班
public class Solution {
    /**
     * @param num a string
     * @return true if a number is strobogrammatic or false
     */
    public boolean isStrobogrammatic(String num) {
        // Write your code here
        int[] map = new int[256];
        map['0'] = '0';
        map['1'] = '1';
        map['6'] = '9';
        map['8'] = '8';
        map['9'] = '6';
        for (int i = 0; i < num.length(); i++) {
            int j = num.length() - i - 1;
            if (map[num.charAt(i)] != num.charAt(j)) {
                return false;
            }
        }
        return true;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)