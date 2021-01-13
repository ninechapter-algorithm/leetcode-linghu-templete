# 逆波兰表达式求值
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/evaluate-reverse-polish-notation/?utm_source=sc-github-wzz)
 ## 题目描述
 求[逆波兰表达式](https://zh.wikipedia.org/zh-hans/%E9%80%86%E6%B3%A2%E5%85%B0%E8%A1%A8%E7%A4%BA%E6%B3%95)的值。

在逆波兰表达法中，其有效的运算符号包括 `+`, `-`, `*`, `/` 。每个运算对象可以是**整数**，也可以是另一个逆波兰计数表达。
 ### 样例说明
 **样例 1:**

```
输入: ["2", "1", "+", "3", "*"] 
输出: 9
解释: ["2", "1", "+", "3", "*"] -> (2 + 1) * 3 -> 9
```

**样例 2:**

```
输入: ["4", "13", "5", "/", "+"]
输出: 6
解释: ["4", "13", "5", "/", "+"] -> 4 + 13 / 5 -> 6
```
 ### 参考代码
 逆波兰表达式是更利于计算机运算的表达式形式, 需要用到栈(先进后出的数据结构).

遍历表达式:

- 碰到数字则入栈
- 碰到运算符则连续从栈中取出2个元素, 使用该运算符运算然后将结果入栈

最后栈中剩余一个数字, 就是结果.
```java
public class Solution {
    public int evalRPN(String[] tokens) {
        Stack<Integer> s = new Stack<Integer>();
        String operators = "+-*/";
        for (String token : tokens) {
            if (!operators.contains(token)) {
                s.push(Integer.valueOf(token));
                continue;
            }

            int a = s.pop();
            int b = s.pop();
            if (token.equals("+")) {
                s.push(b + a);
            } else if(token.equals("-")) {
                s.push(b - a);
            } else if(token.equals("*")) {
                s.push(b * a);
            } else {
                s.push(b / a);
            }
        }
        return s.pop();
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)