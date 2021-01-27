# 编码和解码字符串
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/strings-serialization/?utm_source=sc-github-wzz)
 ## 题目描述
 设计一个将字符串列表编码为字符串的算法。 已经编码的字符串之后会通过网络发送同时也会被解码回到原始的字符串列表。
请实现 `encode` 和 `decode` 
 ### 样例说明
 
 ### 参考代码
 仿照转义字符的表示方法：用":;"表示字符串连接符，"::"表示":"自己本身
```java
public class Solution {
    /**
     * @param strs a list of strings
     * @return encodes a list of strings to a single string.
     */
    public String encode(List<String> strs) {
        // Write your code here
        StringBuilder result = new StringBuilder();
        for(String str : strs){
            result.append(String.valueOf(str.length()) + "$");
            result.append(str);
        }
        return result.toString();
    }

    /**
     * @param str a string
     * @return dcodes a single string to a list of strings
     */
    public List<String> decode(String str) {
        // Write your code here
        List<String> result = new LinkedList<String>();
        int start = 0;
        while(start < str.length()){
            int idx = str.indexOf('$', start);
            int size = Integer.parseInt(str.substring(start, idx));
            result.add(str.substring(idx + 1, idx + size + 1));
            start = idx + size + 1;
        }
        return result;
    }
}

// version: 高频题班
public class Solution {
    /**
     * @param strs a list of strings
     * @return encodes a list of strings to a single string.
     */
    public String encode(List<String> strs) {
        // Write your code here
        StringBuilder ans = new StringBuilder();
        for (String s : strs) {
            for (char c : s.toCharArray()) {
                if (c == ':') {                  // : itself
                    ans.append("::");
                } else {                         //ordinary character
                    ans.append(c);
                }
            }
            ans.append(":;");                    // ; connector
        }
        return ans.toString();
    }

    /**
     * @param str a string
     * @return dcodes a single string to a list of strings
     */
    public List<String> decode(String str) {
        // Write your code here
        List<String> ans = new ArrayList<>();
        char[] sc = str.toCharArray();
        StringBuilder item = new StringBuilder();
        int i = 0;
        while (i < str.length()) {
            if (sc[i] == ':') {                  //escape
                if (sc[i + 1] == ';') {          // ; connector
                    ans.add(item.toString());
                    item = new StringBuilder();
                    i += 2;
                } else {                         // : itself
                    item.append(sc[i + 1]);
                    i += 2;
                }
            } else {                             //ordinary character
                item.append(sc[i]);
                i += 1;
            }
        }
        return ans;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)