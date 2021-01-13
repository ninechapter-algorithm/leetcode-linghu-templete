# 形状工厂
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/shape-factory/?utm_source=sc-github-wzz)
 ## 题目描述
 工厂模式是一种常见的设计模式。实现一个形状工厂 `ShapeFactory` 来创建不同的形状类。这里我们假设只有三角形，正方形和矩形三种形状。
 ### 样例说明
 例1:
```
输入:
ShapeFactory sf = new ShapeFactory();
Shape shape = sf.getShape("Square");
shape.draw();
输出:
  ----
 |    |
 |    |
  ----
```
例2:
```
输入:
ShapeFactory sf = new ShapeFactory();
shape = sf.getShape("Triangle");
shape.draw();
输出:
   /\
  /  \
 /____\
```
例3:
```

输入:
ShapeFactory sf = new ShapeFactory();
shape = sf.getShape("Rectangle");
shape.draw();
输出:
  ----
 |    |
  ----
```
 ### 参考代码
 直接根据对应类型输出对应形状即可
```java
/**
 * Your object will be instantiated and called as such:
 * ShapeFactory sf = new ShapeFactory();
 * Shape shape = sf.getShape(shapeType);
 * shape.draw();
 */
interface Shape {
    void draw();
}

class Rectangle implements Shape {
    // Write your code here
    @Override
    public void draw() {
        System.out.println(" ---- ");
        System.out.println("|    |");
        System.out.println(" ---- ");
   }
}

class Square implements Shape {
    // Write your code here
   @Override
   public void draw() {
        System.out.println(" ---- ");
        System.out.println("|    |");
        System.out.println("|    |");
        System.out.println(" ---- ");
   }
}

class Triangle implements Shape {
    // Write your code here
   @Override
   public void draw() {
        System.out.println("  /\\");
        System.out.println(" /  \\");
        System.out.println("/____\\");
   }
}

public class ShapeFactory {
    /**
     * @param shapeType a string
     * @return Get object of type Shape
     */
    public Shape getShape(String shapeType) {
        // Write your code here
        if (shapeType == null) {
            return null;
        }		
        if (shapeType.equalsIgnoreCase("Triangle")) {
            return new Triangle();
        } else if(shapeType.equalsIgnoreCase("Rectangle")) {
            return new Rectangle();         
        } else if(shapeType.equalsIgnoreCase("Square")) {
            return new Square();
        }
        return null;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)