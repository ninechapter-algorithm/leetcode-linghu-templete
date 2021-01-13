# 恢复IP地址
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/restore-ip-addresses/?utm_source=sc-github-wzz)
 ## 题目描述
 给一个由数字组成的字符串。求出其可能恢复为的所有IP地址。

(你的任务就是往这段字符串中添加三个点, 使它成为一个合法的IP地址. 返回所有可能的IP地址.)
 ### 样例说明
 **样例 1:**

```
输入: "25525511135"
输出: ["255.255.11.135", "255.255.111.35"]
解释: ["255.255.111.35", "255.255.11.135"] 同样可以.
```

**样例 2:**

```
输入: "1116512311"
输出: ["11.165.123.11","111.65.123.11"]
```
 ### 参考代码
 详见九章算法微博: [http://weibo.com/3948019741/BwVKqsKIO](http://weibo.com/3948019741/BwVKqsKIO)
```java
public class Solution {
    public ArrayList<String> restoreIpAddresses(String s) {
        ArrayList<String> result = new ArrayList<String>();
        ArrayList<String> list = new ArrayList<String>();
        
        if (s.length() < 4 || s.length() > 12)
            return result;
        
        helper(result, list, s , 0);
        return result;
    }
    
    public void helper(ArrayList<String> result, ArrayList<String> list, String s, int start) {
        if (list.size() == 4) {
            if (start != s.length())
                return;
            
            StringBuffer sb = new StringBuffer();
            for (String tmp: list) {
                sb.append(tmp);
                sb.append(".");
            }
            sb.deleteCharAt(sb.length()-1);
            result.add(sb.toString());
            return;
        }
        
        for (int i = start; i < s.length() && i < start + 3; i++) {
            String tmp = s.substring(start, i + 1);
            if (isvalid(tmp)) {
                list.add(tmp);
                helper(result, list, s, i+1);
                list.remove(list.size() - 1);
            }
        }
    }
    
    private boolean isvalid(String s) {
        if (s.charAt(0) == '0')
            return s.equals("0"); 		// to eliminate cases like "00", "10"
        int digit = Integer.valueOf(s);
        return digit >= 0 && digit <= 255;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)