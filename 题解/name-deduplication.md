# 姓名去重
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/name-deduplication/?utm_source=sc-github-wzz)
 ## 题目描述
 给一串名字，将他们去重之后返回。两个名字重复是说在忽略大小写的情况下是一样的。
 ### 样例说明
 例1: 
```
输入:["James", "james", "Bill Gates", "bill Gates", "Hello World", "HELLO WORLD", "Helloworld"]


输出:["james", "bill gates", "hello world", "helloworld"]
```
例2: 
```
输入:["cmy","Cmy"]

输出:["cmy"]
```
 ### 参考代码
 利用map去重
```cpp
#include <algorithm>
class Solution {
public:
    /**
     * @param names a string array
     * @return a string array
     */
    vector<string> nameDeduplication(vector<string>& names) {
        // Write your code here
        map<string, bool> mp;
        vector<string> result;
        for (auto& str : names) {
            std::transform(str.begin(), str.end(), str.begin(), ::tolower);
            if (mp.find(str) == mp.end()) {
                mp[str] = true;
                result.push_back(str);
            }
        }
        return result;
    }
};
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)