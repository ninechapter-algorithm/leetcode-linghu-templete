# 学号
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/student-id/?utm_source=sc-github-wzz)
 ## 题目描述
 实现一个名为`Class`的类，包含如下的一些属性和方法：

1. 一个public的students属性，是一个Student类的数组。
2. 一个构造函数，接受一个参数n，代表班级里有n个学生。构造函数需要创建n个学生的实例对象并放在students这个成员中，每个学生按照创建的顺序，学号需要依次标记为0, 1, 2 ... n-1。
 ### 样例说明
 **样例1:**

```plain
输入: 3
输出: [0, 1, 2]
样例说明: 对于3个学生的情况，我们应该让cls.students[0] = 0，cls.students[1] = 1，cls.students[2] = 2
```

**样例2:**

```plain
输入: 5
输出: [0, 1, 2, 3, 4]
```




 ### 参考代码
 添加students属性和Class构造函数，时间复杂度O(n)，空间复杂度O(n)
```python
# Solution 1
class Student:
    def __init__(self, id):
        self.id = id;

class Class:

    '''
     * Declare a constructor with a parameter n which is the total number of
     * students in the *class*. The constructor should create n Student
     * instances and initialized with student id from 0 ~ n-1
    '''
    # write your code here
    def __init__(self, n):
        self.students = []
        for i in range(n): 
            self.students.append(Student(i))

# Solution 2
class Student:
    def __init__(self, id):
        self.id = id;

class Class:

    '''
     * Declare a constructor with a parameter n which is the total number of
     * students in the *class*. The constructor should create n Student
     * instances and initialized with student id from 0 ~ n-1
    '''
    # write your code here
    def __init__(self, n):
        self.students = [Student(i) for i in range(n)]
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)