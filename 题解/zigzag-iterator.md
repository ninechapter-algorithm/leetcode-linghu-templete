# 左旋右旋迭代器
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/zigzag-iterator/?utm_source=sc-github-wzz)
 ## 题目描述
 给你两个一维向量，实现一个迭代器，交替返回两个向量的元素
 ### 样例说明
 **样例1**

```
输入: v1 = [1, 2] 和 v2 = [3, 4, 5, 6]
输出: [1, 3, 2, 4, 5, 6]
解释:
一开始轮换遍历两个数组，当v1数组遍历完后，就只遍历v2数组了，所以返回结果:[1, 3, 2, 4, 5, 6]
```

**样例2**

```
输入: v1 = [1, 1, 1, 1] 和 v2 = [3, 4, 5, 6]
输出: [1, 3, 1, 4, 1, 5, 1, 6]
```
 ### 参考代码
 双指针水题，用双指针求解即可，交叉返回两数组当前位置的数，当一个数组被访问完后，就一直访问另一个数组
```java
public class ZigzagIterator {
    
    public Iterator<Integer> it1;
    public Iterator<Integer> it2;
    public int turns;

    /**
     * @param v1 v2 two 1d vectors
     */
    public ZigzagIterator(List<Integer> v1, List<Integer> v2) {
        // initialize your data structure here.
        this.it1 = v1.iterator();
        this.it2 = v2.iterator();
        turns = 0;
    }

    public int next() {
        // Write your code here
        turns++;
        if((turns % 2 == 1 && it1.hasNext()) || (!it2.hasNext())) {
            return it1.next();
        } else if((turns % 2 == 0 && it2.hasNext()) || (!it1.hasNext())) {
            return it2.next();
        }
        return -1;  
    }

    public boolean hasNext() {
        // Write your code here
        return it1.hasNext() || it2.hasNext();        
    }
}

/**
 * Your ZigzagIterator object will be instantiated and called as such:
 * ZigzagIterator solution = new ZigzagIterator(v1, v2);
 * while (solution.hasNext()) result.add(solution.next());
 * Output result
 */
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)