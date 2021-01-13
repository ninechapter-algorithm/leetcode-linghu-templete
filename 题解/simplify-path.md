# 简化路径
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/simplify-path/?utm_source=sc-github-wzz)
 ## 题目描述
 给定一个文件的绝对路径(Unix-style)，请进行路径简化。

Unix中, `.` 表示当前目录, `..` 表示父目录。

结果必须以 `/` 开头，并且两个目录名之间有且只有一个 `/`。最后一个目录名(如果存在)后不能出现  `/` 。你需要保证结果是正确表示路径的最短的字符串。
 ### 样例说明
 **样例 1:**

```
输入: "/home/"
输出: "/home"
```

**样例 2:**

```
输入: "/a/./../../c/"
输出: "/c"
解释: "/" 没有上级目录, "/../" 的结果就是 "/".
```
 ### 参考代码
 用栈处理即可.

将原字符串以 `'/'` 分隔, 然后遍历:

- 遇到正常的目录名, 入栈
- 遇到 `'.'` 或 空名称 (对应 `"//"`) 则忽略
- 遇到 `".."` 则从栈顶弹出一个元素 (如果栈为空则不弹栈, 对应 `"/../"`)

最后将栈中的元素以 `'/'` 连接得到结果.
```python
class Solution:
    """
    @param path: the original path
    @return: the simplified path
    """
    def simplifyPath(self, path):
        path = path.split('/')
        stack = []
        for i in path:
            if i == '..':
                if len(stack):
                    stack.pop()
            elif i != '.' and i != '':
                stack.append(i)
        return '/' + '/'.join(stack)
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)