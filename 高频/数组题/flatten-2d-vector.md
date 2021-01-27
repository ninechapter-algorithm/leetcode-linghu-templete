# 摊平二维向量
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/flatten-2d-vector/?utm_source=sc-github-wzz)
 ## 题目描述
 设计一个迭代器来实现摊平二维向量的功能
 ### 样例说明
 例1:
```
输入:[[1,2],[3],[4,5,6]]
输出:[1,2,3,4,5,6]
```
例2:
```
输入:[[7,9],[5]]
输出:[7,9,5]
```

 ### 参考代码
 记录横纵坐标。这个版本的代码复杂一些，但是无所谓 next 和 hasNext 的调用顺序和次数。
```python
class Vector2D(object):

    # @param vec2d {List[List[int]]}
    def __init__(self, vec2d):
        self.vec2d = vec2d
        self.row, self.col = 0, -1
        self.next_elem = None

    # @return {int} a next element
    def next(self):
        if self.next_elem is None:
            self.hasNext()
            
        temp, self.next_elem = self.next_elem, None
        return temp

    # @return {boolean} true if it has next element
    # or false
    def hasNext(self):
        if self.next_elem:
            return True
        
        self.col += 1
        while self.row < len(self.vec2d) and self.col >= len(self.vec2d[self.row]):
            self.row += 1
            self.col = 0
            
        if self.row < len(self.vec2d) and self.col < len(self.vec2d[self.row]):
            self.next_elem = self.vec2d[self.row][self.col]
            return True
            
        return False
        

# Your Vector2D object will be instantiated and called as such:
# i, v = Vector2D(vec2d), []
# while i.hasNext(): v.append(i.next())
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)