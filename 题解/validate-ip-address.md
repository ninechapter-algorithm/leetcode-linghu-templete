# 检验IP地址
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/validate-ip-address/?utm_source=sc-github-wzz)
 ## 题目描述
 实现一个函数来检查输入字符串是一个合法的IPv4地址，还是一个合法的IPv6地址，抑或是两者都不是。

**IPv4**地址被规范地表示为点分十进制，包含四个取值为0到255的十进制数，其间使用点号(".")来进行分隔，例如，`172.16.254.1`；

此外，前导零在IPv4地址中是非法的。例如，地址`172.16.254.01`就是非法的。

**IPv6**地址被表示为十六进制数位，每4个十六进制数位归为一组，共八组，每组可表示16个二进制位。每组之间使用冒号(":")来进行分隔。例如，地址`2001:0db8:85a3:0000:0000:8a2e:0370:7334`是合法的。同时，去掉每组十六进制数位中的一些前导零，或是将表示十六进制数位的小写字母写作大写字母，也都是合法的，所以`2001:db8:85a3:0:0:8A2E:0370:7334`同样是一个合法的IPv6地址（它忽略了前导零同时使用了大写字母）。

然而，我们不能为了追求简洁就使用两个冒号("::")将连续的值为0的组替换为一个空组。例如，`2001:0db8:85a3::8A2E:0370:7334`就是一个非法的IPv6地址。

此外，额外的前导零在IPv6中也是非法的。例如，地址`02001:0db8:85a3:0000:0000:8a2e:0370:7334`就是非法的。
 ### 样例说明
 例1:
```
输入："172.16.254.1"

输出："IPv4"

说明：这是一个合法的IPv4地址，因此返回"IPv4"。
```

例2:
```
输入："2001:0db8:85a3:0:0:8A2E:0370:7334"

输出："IPv6"

说明：这是一个合法的IPv6地址，因此返回"IPv6"。
```

例3:
```
输入："256.256.256.256"

输出："Neither"

说明：这既不是一个合法的IPv4地址，也不是一个合法的IPv6地址，因此返回"Neither"。
```
 ### 参考代码
 字符串处理题，要注意特殊情况的判断。
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
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)