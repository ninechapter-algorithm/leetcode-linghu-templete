# 单例
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/singleton/?utm_source=sc-github-wzz)
 ## 题目描述
 **单例** 是最为最常见的设计模式之一。对于任何时刻，如果某个类只存在且最多存在一个具体的实例，那么我们称这种设计模式为单例。例如，对于 class Mouse (不是动物的mouse哦)，我们应将其设计为 singleton 模式。

你的任务是设计一个 `getInstance` 方法，对于给定的类，每次调用 `getInstance` 时，都可得到同一个实例。
 ### 样例说明
 ```
在 Java 中:

	A a = A.getInstance();
	A b = A.getInstance();

a 应等于 b.

```
 ### 参考代码
 创建私有静态成员对象，每次获取时返回此对象。
```java
class Solution {
    
    
    /**
     * @return: The same instance of this class every time
     */
    public static Solution instance = null;
    public static Solution getInstance() {
        if (instance == null) {
            instance = new Solution();
        }
        return instance;
    }
};
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)