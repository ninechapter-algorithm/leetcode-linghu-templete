# 将数字转换为16进制
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/convert-a-number-to-hexadecimal/?utm_source=sc-github-wzz)
 ## 题目描述
 给定一个整数，写一个函数将其转换为16进制。对于负整数，需要使用[**二进制补码**](https://en.wikipedia.org/wiki/Two%27s_complement "")。
 ### 样例说明
 **样例1**
```
输入：26
输出："1a"
```
**样例2**
```
输入：-1
输出："ffffffff"
```
 ### 参考代码
 辗转相除求十六进制
```java
// 方法一
public class Solution {
    public String toHex(int num) {
        if(num == 0) {
            return "0";
        }
        String ans = "";
        int len = 0;
        while(num != 0 && len < 8) {
            //15的二进制：1111
            int bit = num & 15;
            if(bit < 10) {
                //0 - 9
                ans = (char)('0' + bit) + ans;
            }
            else {
                //a - f
                ans = (char)('a' + bit - 10) + ans;
            }
            //位运算，对二进制的num右移4位相当于除以16
            num >>= 4;
            len++;
        }
        return ans;
    }
}

// 方法二：普通的辗转相除，区分正负整数分别计算
public class Solution {
    public String toHex(int num) {
        if(num == 0) {
            return "0";
        }
        int bit[] = new int[10];
        int len = 0;
        String ans = "";
        for(int i=0; i<9; i++) {
            bit[i] = 0;
        }
        long n = num;
        n = n > 0? n : -n;
        while(n > 0) {
            bit[len++] = (int)n % 16;
            n /= 16;
        }
        if(num < 0) {
            for(int i=0; i<8; i++)
            {
                bit[i] = 15 - bit[i];
            }
            int pos = 0;
            while(bit[pos] == 15)
            {
                bit[pos] = 0;
                pos++;
            }
            bit[pos]++;
        }
        int leader0 = 1;
        for(int i=7; i>=0; i--)
        {    
            if(bit[i] != 0) leader0 = 0;
            if(leader0 == 1) continue;
            if(bit[i] < 10) ans += (char)('0' + bit[i]);
            else ans += (char)('a' + bit[i] - 10);
        }
        return ans;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)