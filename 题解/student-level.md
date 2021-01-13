# 成绩等级
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/student-level/?utm_source=sc-github-wzz)
 ## 题目描述
 实现一个学生的类 `Student`. 包含如下的成员函数和方法：

1. 两个公有成员 `name` 和 `score`。分别是字符串类型和整数类型。
2. 一个构造函数，接受一个参数 `name`。
3. 一个公有成员函数 `getLevel()` 返回学生的成绩等级（一个字符）。

等级表如下：

* A: score >= 90
* B: score >= 80 and < 90
* C: score >= 60 and < 80
* D: score < 60
 ### 样例说明
 **样例 1：**
```
Java:
    Student student = new Student("Zuck");
    student.score = 10;
    student.getLevel(); // should be 'D'
    student.score = 60;
    student.getLevel(); // should be 'C'
```
**样例 2：**
```
Python:
    student = Student("Zuck")
    student.score = 10
    student.getLevel() # should be 'D'
    student.score = 60
    student.getLevel() # should be 'C'
```
 ### 参考代码
 ```java
public class Student {
    /**
     * Declare two public attributes name(string) and score(int).
     */
    public String name;
    public int score;
    
    /**
     * Declare a constructor expect a name as a parameter.
     */
    public Student(String name) {
        this.name = name;
    }
    
    /**
     * Declare a public method `getLevel` to get the level(char) of this student.
     */
    public char getLevel() {
        if (score >= 90) {
            return 'A';
        } else if (score >= 80) {
            return 'B';
        } else if (score >= 60) {
            return 'C';
        } else {
            return 'D';
        }
    }
}

```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)