# 玩具工厂
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/toy-factory/?utm_source=sc-github-wzz)
 ## 题目描述
 工厂模式是一种常见的设计模式。请实现一个玩具工厂 `ToyFactory` 用来产生不同的玩具类。可以假设只有猫和狗两种玩具。

 ### 样例说明
 
例1：
```
输入：
ToyFactory tf = ToyFactory();
Toy toy = tf.getToy('Dog');
toy.talk(); 
输出：
Wow
```
例2:
```
输入：
ToyFactory tf = ToyFactory();
toy = tf.getToy('Cat');
toy.talk();
输出：
Meow

```
 ### 参考代码
 设计两个子类继承父类即可
```java
/**
 * Your object will be instantiated and called as such:
 * ToyFactory tf = new ToyFactory();
 * Toy toy = tf.getToy(type);
 * toy.talk();
 */
interface Toy {
    void talk();
}

class Dog implements Toy {
    // Write your code here
    @Override
    public void talk() {
        System.out.println("Wow");
   }
}

class Cat implements Toy {
    // Write your code here
    @Override
    public void talk() {
        System.out.println("Meow");
   }
}

public class ToyFactory {
    /**
     * @param type a string
     * @return Get object of the type
     */
    public Toy getToy(String type) {
        // Write your code here
        if (type == null) {
            return null;
        }		
        if (type.equalsIgnoreCase("Dog")) {
            return new Dog();
        } else if(type.equalsIgnoreCase("Cat")) {
            return new Cat();         
        }
        return null;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)