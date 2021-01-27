# 左旋右旋迭代器 II
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/zigzag-iterator-ii/?utm_source=sc-github-wzz)
 ## 题目描述
 *k* 个一维向量，循环地返回向量中的元素
 ### 样例说明
 **样例1**

```
输入: k = 3
vecs = [
    [1,2,3],
    [4,5,6,7],
    [8,9],
]
输出: [1,4,8,2,5,9,3,6,7]
```

**样例2**

```
输入: k = 3
vecs = [
    [1,1,1]
    [2,2,2]
    [3,3,3]
]
输出: [1,2,3,1,2,3,1,2,3]
```
 ### 参考代码
 用k个指针维护每个数组的当前最靠前的元素，循环枚举这k个指针，每次枚举到就在答案序列中将该数加入，如果指针到了该数组的尾部，那么就不作处理
```python
class ZigzagIterator2:

    # @param {int[][]} a list of 1d vectors
    def __init__(self, vecs):
        # initialize your data structure here
        self.queue = [v for v in vecs if v]


    def next(self):
        # Write your code here
        v = self.queue.pop(0)
        value = v.pop(0)
        if v:
            self.queue.append(v)
        return value


    def hasNext(self):
        # Write your code here
        return len(self.queue) > 0
        

# Your ZigzagIterator2 object will be instantiated and called as such:
# solution, result = ZigzagIterator2(vecs), []
# while solution.hasNext(): result.append(solution.next())
# Output result
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)