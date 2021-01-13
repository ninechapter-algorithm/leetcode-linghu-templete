# 宠物收养所
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/animal-shelter/?utm_source=sc-github-wzz)
 ## 题目描述
 在一个宠物避难所里，仅有`狗`和`猫`两种动物可供领养，且领养时严格执行`“先进先出”`的规则。如果有人想要从避难所领养动物，他只有两种选择：要么选择领养所有动物中`最资深`的一只（根据到达避难所的时间，越早到的越资深），要么选择领养猫或狗（同样，也只能领养最资深的一只）。也就是说，领养者不能随意选择某一指定动物。请建立一个数据结构，使得它可以运行以上规则，并可实现 `enqueue`, `dequeueAny`, `dequeueDog`， 和 `dequeueCat` 操作。 

建议使用 `LinkedList` 作为数据结构实现。
 ### 样例说明
 
 ### 参考代码
 我们可以用两个队列实现，分别代表猫和狗，每次取的时候看两个顶端哪个出现的早
```java
public class AnimalShelter {

    public AnimalShelter() {
        // do initialize if necessary
        tot = 0;
        dogs = new LinkedList<String>();
        cats = new LinkedList<String>();
    }

    /**
     * @param name a string
     * @param type an integer, 1 if Animal is dog or 0
     * @return void
     */
    void enqueue(String name, int type) {
        // write your code here
        tot += 1;
        if (type == 1)
            dogs.add(tot + "#" + name);
        else
            cats.add(tot + "#" + name);
    }

    public String dequeueAny() {
        // write your code here
        if (cats.isEmpty())
            return dequeueDog();
        else if (dogs.isEmpty())
            return dequeueCat();
        else {
            int d_time = getTime(dogs.getFirst());
            int c_time = getTime(cats.getFirst());
            if (c_time < d_time)
                return dequeueCat();
            else
                return dequeueDog();
        }
    }

    public String dequeueDog() {
        // write your code here
        String name = getName(dogs.getFirst());
        dogs.removeFirst();
        return name;
    }

    public String dequeueCat() {
        // write your code here
        String name = getName(cats.getFirst());
        cats.removeFirst();
        return name;
    }

    private int tot;
    private LinkedList<String> cats, dogs;
    private String getName(String str) {
        return str.substring(str.indexOf("#") + 1, str.length());
    }
    private int getTime(String str) {
        return Integer.parseInt(str.substring(0, str.indexOf("#")));
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)