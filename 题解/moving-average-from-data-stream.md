# 数据流滑动窗口平均值
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/moving-average-from-data-stream/?utm_source=sc-github-wzz)
 ## 题目描述
 给出一串整数流和窗口大小，计算滑动窗口中所有整数的平均值。
 ### 样例说明
 **样例1 :**
```
MovingAverage m = new MovingAverage(3);
m.next(1) = 1 // 返回 1.00000
m.next(10) = (1 + 10) / 2 // 返回 5.50000
m.next(3) = (1 + 10 + 3) / 3 // 返回 4.66667
m.next(5) = (10 + 3 + 5) / 3 // 返回 6.00000
```
 ### 参考代码
 使用队列
```java
public class MovingAverage {

    private Queue<Integer> que;
    private double sum = 0;
    private int size;

    /** Initialize your data structure here. */
    public MovingAverage(int size) {
        que = new LinkedList<Integer>();
        this.size = size;
    }
    
    public double next(int val) {
        // Write your code here
        sum += val;
        if (que.size() == size) {
            sum = sum - que.poll();
        }
        que.offer(val);
        return sum / que.size();
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)