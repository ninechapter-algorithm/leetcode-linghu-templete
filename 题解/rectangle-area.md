# 矩阵面积
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/rectangle-area/?utm_source=sc-github-wzz)
 ## 题目描述
 实现一个矩阵类`Rectangle`，包含如下的一些成员变量与函数：

1. 两个共有的成员变量 `width` 和 `height` 分别代表宽度和高度。
1. 一个构造函数，接受2个参数 width 和 height 来设定矩阵的宽度和高度。
2. 一个成员函数 `getArea`，返回这个矩阵的面积。
 ### 样例说明
 ```
样例1:
Java:
    Rectangle rec = new Rectangle(3, 4);
    rec.getArea(); // should get 12，3*4=12

Python:
    rec = Rectangle(3, 4)
    rec.getArea()

样例2:
Java:
    Rectangle rec = new Rectangle(4, 4);
    rec.getArea(); // should get 16，4*4=16

Python:
    rec = Rectangle(4, 4)
    rec.getArea()
```
 ### 参考代码
 Python课题解 简单的实现类的函数。。。。。。。。。。。
```python
class Rectangle:

    '''
     * Define a constructor which expects two parameters width and height here.
    '''
    # write your code here
    #初始化
    def __init__(self, width, height):
        self.width = width
        self.height = height
    
    '''
     * Define a public method `getArea` which can calculate the area of the
     * rectangle and return.
    '''
    # write your code here
    #返回矩阵面积
    def getArea(self):
        return self.width * self.height
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)