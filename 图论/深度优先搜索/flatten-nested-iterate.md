# flatten nested iterate
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/flatten-nested-iterate/?utm_source=sc-github-wzz)
 ## 题目描述
 1753
 ### 样例说明
 1753
 ### 参考代码
 ```python
def flattern(A):
    result = []
    sta = list()
    for ele in reversed(A):
        sta.append(ele)
    while len(sta) > 0:
        ele = sta[-1]
        sta.pop()
        if isinstance(ele, int):
            result.append(ele)
        else:
            for sub_ele in reversed(ele):
                sta.append(sub_ele)
    return result
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)