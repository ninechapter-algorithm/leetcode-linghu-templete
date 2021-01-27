# 最长有效括号
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/longest-valid-parentheses/?utm_source=sc-github-wzz)
 ## 题目描述
 <p><span style="line-height: 30px;">给出一个只包含</span><code style="font-size: 12.6000003814697px; white-space: normal; line-height: 30px;">'('</code><span style="line-height: 30px;">&nbsp;和</span><code style="font-size: 12.6000003814697px; white-space: normal; line-height: 30px;">')'</code><span style="line-height: 30px;">的字符串，找出其中最长的左右括号正确匹配的合法子串。</span><br></p>
 ### 样例说明
 **样例 1:**

```
输入: "(()"
输出: 2
解释: 最长有效括号子串为 "()"
```

**样例 2:**

```
输入: ")()())"
输出: 4
解释: 最长有效括号子串为 "()()"
```
 ### 参考代码
 Given a string containing just the characters '(' and ')', find the length of the longest valid (well-formed) parentheses substring.&nbsp;<div><br></div><div>&nbsp;For "(()", the longest valid parentheses substring is "()", which has length = 2.&nbsp;</div><div><br></div><div>&nbsp;Another example is ")()())", where the longest valid parentheses substring is "()()", which has length = 4.</div><div><br></div><div><span style="color: rgb(102, 110, 112); font-family: 'Open Sans', Arial, sans-serif; line-height: 22.3999996185303px;">详细题解请见九章算法微博:&nbsp;</span><font color="#666e70" face="Open Sans, Arial, sans-serif"><span style="line-height: 22.3999996185303px;"><a href="http://weibo.com/3948019741/Bxp24fkup" target="_blank">http://weibo.com/3948019741/Bxp24fkup</a></span></font><br></div>

考点：
* 栈
* dp

题解：

1.遍历给字符串中的所有字符
1.1若当前字符s[index]为左括号'('，将当前字符下标index入栈（下标稍后有其他用处），处理下一字符
1.2若当前字符s[index]为右括号')'，判断当前栈是否为空
1.2.1若栈为空，则accumulatedLen = 0，当前有效长度为0，处理下一字符（当前字符右括号下标不入栈）
1.2.2若栈不为空，则出栈（由于仅左括号入栈，则出栈元素对应的字符一定为左括号，可与当前字符右括号配对），判断栈是否为空
1.2.2.1若栈为空，则maxlen = max(maxlen, index-start+1)，更新当前最大匹配序列长度
1.2.2.2若栈不为空，则maxlen = max(maxlen, i-栈顶元素值)，更新当前最大匹配序列长度
```java
public class Solution {
    public int longestValidParentheses(String s) {

        if (s == null) {
            return 0;
        }

        Stack<Integer> stack = new Stack<Integer>();
        int maxLen = 0;
        int accumulatedLen = 0;

        for(int i = 0; i < s.length(); i++) {
            if (s.charAt(i) == '(') {
                stack.push(i);
            } else {
                if (stack.isEmpty()) {   //如果栈为空，没有左括号可以匹配
                    accumulatedLen = 0;
                } else {
                    int matchedPos = stack.pop(); //从最近的'('作为起点
                    int matchedLen = i - matchedPos + 1;	//计算两括号间的长度

                    if (stack.isEmpty()) {			//如果栈为空，没有左括号可以匹配
                        accumulatedLen += matchedLen;	
                        matchedLen = accumulatedLen;	//更新当前匹配括号序列长度
                    } else {
                        matchedLen = i - stack.peek();  
                    }

                    maxLen = Math.max(maxLen, matchedLen);
                }
            }
        }

        return maxLen;
   }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)