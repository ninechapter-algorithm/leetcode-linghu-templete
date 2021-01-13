# 栈排序
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/stack-sorting/?utm_source=sc-github-wzz)
 ## 题目描述
 请设计一种方法将一个栈进行升序排列 （最大的数在最上面）。

你可以使用另外一个栈来辅助操作，但不可将这些数复制到另外一个数据结构中 （如，数组）。
 ### 样例说明
 给一个栈：
```
| |
|3|
|1|
|2|
|4|
 -
```

排序之后：
```
| |
|4|
|3|
|2|
|1|
 -
```

栈会被序列化为`[4,2,1,3]`，也就是说最右边是栈顶。
 ### 参考代码
 ```cpp
class Solution {
public:
    /**
     * @param stk an integer stack
     * @return void
     */
    void stackSorting(stack<int>& stk) {
        // Write your code here
        stack<int> tmp;
        while (!stk.empty()) {
            if (!stk.empty() && (tmp.empty() || tmp.top() >= stk.top())) {
                tmp.push(stk.top());
                stk.pop();
            }
            else {
                int value = stk.top(); stk.pop();
                while (!tmp.empty() && tmp.top() <= value)  {
                    stk.push(tmp.top());
                    tmp.pop();
                }
                stk.push(value);
                while (!tmp.empty()) {
                    stk.push(tmp.top());
                    tmp.pop();
                }
            }
        }
        while (!tmp.empty()) {
            stk.push(tmp.top());
            tmp.pop();
        }
    }
};
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)