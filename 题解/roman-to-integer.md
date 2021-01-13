# 罗马数字转整数
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/roman-to-integer/?utm_source=sc-github-wzz)
 ## 题目描述
 给定一个罗马数字，将其转换成整数。

输入数据保证返回的结果1到3999的范围内。
 ### 样例说明
 **样例 1:**

```
输入: "IV"
输出: 4
```

**样例 2:**

```
输入: "XCIX"
输出: 99
```
 ### 参考代码
 根据罗马数字的计数规则, 模拟运算即可.
```java
public class Solution {
 	public int romanToInt(String s) {
	    if (s == null || s.length()==0) {
                return 0;
	    }
	    Map<Character, Integer> m = new HashMap<Character, Integer>();
	    m.put('I', 1);
	    m.put('V', 5);
	    m.put('X', 10);
	    m.put('L', 50);
	    m.put('C', 100);
	    m.put('D', 500);
	    m.put('M', 1000);

	    int length = s.length();
	    int result = m.get(s.charAt(length - 1));
	    for (int i = length - 2; i >= 0; i--) {
	        if (m.get(s.charAt(i + 1)) <= m.get(s.charAt(i))) {
	            result += m.get(s.charAt(i));
	        } else {
	            result -= m.get(s.charAt(i));
	        }
	    }
	    return result;
	}
}

///////////////// version: 高频题班

public class Solution {
    /**
     * @param s Roman representation
     * @return an integer
     */
    public int romanToInt(String s) {
        int ans;
        char[] sc = s.toCharArray();
        ans = toInt(sc[0]);                        //0 special
        for (int i = 1; i < s.length(); i++) {
            ans += toInt(sc[i]);
            if (toInt(sc[i - 1]) < toInt(sc[i])) {
                ans -= toInt(sc[i - 1]) * 2;
            }
        }
        return ans;
    }

    int toInt(char s) {
        switch(s) {
            case 'I': return 1;
            case 'V': return 5;
            case 'X': return 10;
            case 'L': return 50;
            case 'C': return 100;
            case 'D': return 500;
            case 'M': return 1000;
        }
        return 0;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)