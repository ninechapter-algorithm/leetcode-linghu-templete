# 引用
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/reference/?utm_source=sc-github-wzz)
 ## 题目描述
 实现一个类 *ReferenceManager* 包含如下两种方法

1.`copyValue(Node obj)` 只拷贝参数*obj*的权值，*obj*和*node*仍然是两个指针

2.`copyReference(Node obj)` *obj*和*node*指向同一个地方
 ### 样例说明
 ```
ReferenceManager ref = ReferenceManager();
Node obj = new Node(0);
ref.copyValue(obj);
ref.node.val; // 值为0
ref.node; // 与obj不同.

Node obj2 = new Node(1);
ref.copyReference(obj2);
ref.node.val; // 值为1
ref.node; // 与 obj2相同，指向同一个地址
```
 ### 参考代码
 java中直接赋值是同一个变量，指向同一个地址
```java
public class ReferenceManager {
    public Node node;

    public void copyValue(Node obj) {
        if (obj == null) {
            return;
        }
        if (node == null) {
            node = new Node(obj.val);
        }
        node.val = obj.val;
    }

    public void copyReference(Node obj) {
        node = obj;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)