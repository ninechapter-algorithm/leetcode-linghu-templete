# 自动补全
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/typeahead/?utm_source=sc-github-wzz)
 ## 题目描述
 实现一个typeahead功能，给出一个字符串和一个字典，包含若干个单词，返回所有含有这个字符串子串的单词；字典不能被修改，并且这个方法可能被调用多次。
 ### 样例说明
 
 ### 参考代码
 ```cpp
class Typeahead {
private:
    map<string, vector<int>> mp;
    vector<string> strs; 
public:
    // @param dict: A dictionary of words dict
    Typeahead(unordered_set<string> &dict) {
        // do initialize if necessary
        int cnt = 0;
        for (string str : dict) {
            strs.push_back(str);
            int len = str.size();
            for (int i = 0; i < len; ++i)
                for (int j = i + 1; j <= len; ++j) {
                    string tmp = str.substr(i, j - i);
                    if (mp.find(tmp) == mp.end()) {
                        mp[tmp] = vector<int>();
                        mp[tmp].push_back(cnt);
                    } else {
                        if (mp[tmp][mp[tmp].size() - 1] != cnt)
                            mp[tmp].push_back(cnt);
                    }
                }
            cnt ++;
        }
    }
    
    // @param str: a string
    // @return a set of words
    vector<string> search(string &str) {
        // Write your code here
        if (mp.find(str) == mp.end()) {
            return vector<string>();
        } else {
            vector<string> results;
            int len = mp[str].size();
            for (int i = 0; i < len; ++i) {
                results.push_back(strs[mp[str][i]]);
            }
            return results;
        }
    }
};
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)