# Getter与Setter
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/setter-and-getter/?utm_source=sc-github-wzz)
 ## 题目描述
 实现一个`School`的类，包含下面的这些属性和方法:

* 一个string类型的私有成员`name`.
* 一个setter方法`setName`，包含一个参数name.
* 一个getter方法`getName`，返回该对象的name。
 ### 样例说明
 ```
Java:
    School school = new School();
    school.setName("MIT");
    school.getName(); // 返回 "MIT" 作为结果 

Python:
    school = School();
    school.setName("MIT")
    school.getName() # 返回 "MIT" 作为结果 
		
```
 ### 参考代码
 面向对象程序设计，name为私有成员，setter和getter是公有成员。
```java
public class School {
    /*
     * Declare a private attribute *name* of type string.
     */
    private String name;
    
    /**
     * Declare a setter method `setName` which expect a parameter *name*.
     */
    public void setName(String name) {
        this.name = name;
    }
    
    /**
     * Declare a getter method `getName` which expect no parameter and return
     * the name of this school
     */
    public String getName() {
        return this.name;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)