# 删除元素
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/remove-element/?utm_source=sc-github-wzz)
 ## 题目描述
 <p>给定一个数组和一个值，在原地删除与值相同的数字，返回新数组的长度。</p><p>元素的顺序可以改变，并且对新的数组不会有影响。</p>
 ### 样例说明
 
 ### 参考代码
 Given an array and a value, remove all instances of that value in place and return the new length.

The order of elements can be changed. It doesn't matter what you leave beyond the new length.

从前往后，遇到等于value的就跳过，把后面的元素填到前面的位置里。
```java
public class Solution {
    public int removeElement(int[] A, int elem) {
        int i = 0;
        int pointer = A.length - 1;
        while(i <= pointer){
            if(A[i] == elem){
                A[i] = A[pointer];
                pointer--;
            } else {
                i++;
            }
        }
        return pointer + 1;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)