# 翻转游戏II
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/flip-game-ii/?utm_source=sc-github-wzz)
 ## 题目描述
 翻转游戏：给定一个只包含两种字符的字符串：`+`和`-`，你和你的小伙伴轮流翻转`"++"`变成`"--"`。当一个人无法采取行动时游戏结束，另一个人将是赢家。

编写一个函数判断是否能够保证先手胜利。
 ### 样例说明
 **样例1**

```
输入: s = "++++"
输出: true
解释:
先手可以通过翻转中间的"++"使字符串变成"+--+"来保证胜利。.
```

**样例2**

```
输入: s = "+++++"
输出: false 
解释:
先手赢不了啊，后手都有应对的方法
"+++--" --> "+----"
"++--+" --> "----+"
```

 ### 参考代码
 ```java
// 方法一 搜索
public class Solution {
    public boolean canWin(String s) {
        boolean[] state = new boolean[s.length()];
        for (int i = 0; i < s.length(); i++) {
            if (s.charAt(i) == '+') {
                state[i] = true;
            } else {
                state[i] = false;
            }
        }
        return search(state);
    }
    public boolean search(boolean[] state) {
        for (int i = 0; i < state.length - 1; i++) {
            if (state[i] && state[i + 1]) {
                state[i] = false;
                state[i + 1] = false;
                if (!search(state)) {
                    state[i] = true;
                    state[i + 1] = true;
                    return true;
                } else {
                    state[i] = true;
                    state[i + 1] = true;
                }
            }
        }
        return false;
    }
}


// 方法二 nim 博弈
public class Solution {
    public boolean canWin(String s) {
        int[] nim = new int[s.length() + 1];
        boolean[] happen = new boolean[s.length() + 1];
        for (int i = 2; i <= s.length(); i++) {
            for (int j = 0; j < i - j - 1; j++) {
                happen[nim[j] ^ nim[i - j - 2]] = true;
            }
            boolean nimEmpty = true;
            for (int j = 0; j <= s.length(); j++) {
                if (!happen[j] && nimEmpty) {
                    nimEmpty = false;
                    nim[i] = j;
                } else {
                    happen[j] = false;
                }
            }
        }
        int ans = 0;
        int len = 0;
        s = s + "-";
        for (int i = 0; i < s.length(); i++) {
            if (s.charAt(i) == '+') {
                len++;
            } else {
                ans = ans ^ nim[len];
                len = 0;
            }
        }
        if (ans == 0) {
            return false;
        } else {
            return true;
        }
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)