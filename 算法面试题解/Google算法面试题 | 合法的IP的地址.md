## 问题描述

编写一个函数判断一个字符串是IPv4地址还是IPv6地址或者两者都不是。

IPv4地址以十进制格式表示，它由四个十进制数组成，每个数字范围从0到255，以点（“.”）分隔，例如172.16.254.1;

IPv6地址以十六进制格式表示，它由八个四位的十六进制数组成，以冒号（“:”）分隔，例如：

2001:0db8:85a3:0000:0000:8a2e:0370:7334就是合法的 IPv6地址。

同时，我们可以省略一些前导零或者把字母以大写字母表示，所以2001:db8:85a3:0:0:8A2E:0370:7334也是合法的IPv6地址。但是不能完全省略0值，比如2001:0db8:85a3::8A2E:0370:7334就不是合法的IPv6地址。

多余的前导零也是不合法的，比如02001:0db8:85a3:0000:0000:8a2e:0370:7334。

你可以假设输入没有额外的空格和特殊符号。 

**样例说明**
```
样例1：
输入: "172.16.254.1"
输出: "IPv4"
样例解释: 这是一个IPv4地址，返回"IPv4".

样例2：
输入:  "2001:0db8:85a3:0:0:8A2E:0370:7334"
输出: "IPv6"
样例解释: 这是一个IPv6地址，返回"IPv6".

样例3：
输入: "256.256.256.256"
输出: "Neither"
样例解释: 这既不是IPv4地址也不是IPv6地址，返回"Neither"
```
## 解题思路

1. 这题是一题字符串处理的题目，题目要求我们判断一个字符串是不是合法的IPv4或IPv6字符串。我们可以把分别考虑这个字符串是不是IPv4字符串或IPv6字符串。

2. 判断一个字符串是不是IPv4字符串比IPv6稍难。
我们从IPv4的特点入手:由4段数字组成，其中有三个'.'符号，每个数字的范围都在0~255之间，且每个数都是合法的数字(没有前导零)。
所以我们可以先把这个字符串用‘.'分隔开，再统计一下'.'的个数，最后判断每个数字是否合法即可。
需要注意的是IPv4字符串的每一个数字不允许存在前导0，但是单个的0是允许的。

3. 判断IPv6的思路和IPv4类似，拆分并且判断分隔符的个数，依次检查每个数的正确性。IPv6的地址不需要判断前导零，但是需要注意大小写都是合法的。 

**参考代码**
```java
public class Solution {
    String IPv6char = "0123456789abcdefABCDEF";
    public boolean isVaild_IPv4Number(String str){
        int num = 0;
        if(str.equals("") || str.length() > 3) {    
            return false;
        }
        if(str.length() > 1 && str.charAt(0) == '0' ) {
            return false;
        }
        for (int i = 0; i < str.length(); ++i){    
            if ( !Character.isDigit(str.charAt(i))) {    
                return false;    
            }
            else num = num * 10 + str.charAt(i)-'0';
        }
        if(num >= 0 && num < 256) {
            return true;
        }
        else return false;
    }
    
    public boolean isVaild_IPv6Number(String str) {
        if(str.equals("") || str.length() > 4) {    
            return false;    
        }  
        for (int i = 0; i < str.length(); ++i) {    
            if ( IPv6char.indexOf(str.charAt(i)) == -1) {    
                return false;    
            }
        }
        return true;
    }
    
    public int NumberOftoken(String IP,char token){
        int num = 0;
        for (int i = 0; i< IP.length(); ++i){
            if( IP.charAt(i) == token) {
                num ++;
            }
        }
        return num;
    }
    public String validIPAddress(String IP) {
        
        String[] IPv4 = IP.split("\\.");
        boolean is_IPv4 = true;
        if(IPv4.length == 4 && NumberOftoken(IP,'.') == 3) {
            for(int i = 0; i < 4; i++) {
                if(!isVaild_IPv4Number(IPv4[i])){
                    is_IPv4 = false;
                    break;
                }
            }
        }
        else is_IPv4 = false ;
        if(is_IPv4)return "IPv4";
        
        String[] IPv6 = IP.split(":");
        boolean is_IPv6 = true;
        if(IPv6.length == 8 && NumberOftoken(IP,':') == 7) {
            for(int i = 0; i < 8; i++){
                if(!isVaild_IPv6Number(IPv6[i])){
                    is_IPv6 = false;
                    break;
                }
                
            }
        }
        else is_IPv6 = false;
        if(is_IPv6)return "IPv6";
        
        return "Neither";
    }
}
```

更多题解参考：[LintCode/LeetCode 参考答案查询](http://www.jiuzhang.com/solution/validate-ip-address/?utm_source=sc-github-lm)

## 面试官角度

这题主要考察字符串处理和corner case的处理能力，题目的要求需要仔细阅读，每一个细节都需要仔细处理。如果能做到bug free，就能获得较高的评价。 

## LintCode相关题目

[417. 有效数字](http://www.lintcode.com/zh-cn/problem/valid-number/?utm_source=sc-github-lm)

[54. 转换字符串到整数](http://www.lintcode.com/zh-cn/problem/string-to-integer-ii/?utm_source=sc-github-lm)


