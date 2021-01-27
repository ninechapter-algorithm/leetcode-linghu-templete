# 移除子串
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/remove-substrings/?utm_source=sc-github-wzz)
 ## 题目描述
 给出一个字符串 `s` 以及 `n` 个子串。你可以从字符串 s 中移除 n 个子串中的任意一个，使得剩下来s的长度最小，输出这个最小长度。
 ### 样例说明
 例1:
```
输入:
"ccdaabcdbb"
["ab","cd"]
输出:
2
解释: 
ccdaabcdbb -> ccdacdbb -> cabb -> cb (length = 2)
```

例2:
```
输入:
"abcabd"
["ab","abcd"]
输出:
0
解释: 
abcabd -> abcd -> "" (length = 0)
```

 ### 参考代码
 利用bfs。
在可以删除的每一个地方，尝试删除。
```cpp
class Solution {
public:
    /**
     * @param s a string
     * @param dict a set of n substrings
     * @return the minimum length
     */
    int minLength(string& s, set<string>& dict) {
        // Write your code here
        queue<string> que;
        unordered_set<string> hash;
    
        int min = s.size();
        que.push(s);
        hash.insert(s);

        while (!que.empty()) {
            string s = que.front();
            que.pop();
            for (auto& sub : dict) {
                int found = s.find(sub);
                while (found != -1) {
                    string new_s = s.substr(0, found) +
                        s.substr(found + sub.size(), s.size() - found - sub.size());
                    if (hash.find(new_s) == hash.end()) {
                        if (new_s.size() < min)
                            min = new_s.size();
                        que.push(new_s);
                        hash.insert(new_s);
                    }
                    found = s.find(sub, found + 1);
                }
            }
        }
        return min;
    }
};
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)