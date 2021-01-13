# 落单的数 III
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/single-number-iii/?utm_source=sc-github-wzz)
 ## 题目描述
 <p>给出2*n + 2个的数字，除其中两个数字之外其他每个数字均出现两次，找到这两个数字。</p>
 ### 样例说明
 
```
样例 1:
	输入:  [1,2,2,3,4,4,5,3]
	输出:  [1,5]

样例 2:
	输入: [1,1,2,3,4,4]
	输出:  [2,3]
	
```

 ### 参考代码
 利用异或运算。
假设两个落单数字是 A、B
$2*n + 2$ 个数字异或，会得到两个仅出现一次的数字的异或结果：xor = A^B。

其中我们取出xor中任何一位1，这里取最低位的1。
这个1一定是A和B中对应位上一个是1一个是0。
所以可以将所有数字分成两类，一类是该位是1的，一类是该位是0的。
分别异或起来就得到A和B了。两类数一定都是奇数个，多出来的一个分别就是A、B。
```java
public class Solution {
    /**
     * @param A : An integer array
     * @return : Two integers
     */
    public List<Integer> singleNumberIII(int[] A) {
        int xor = 0;
        for (int i = 0; i < A.length; i++) {
            xor ^= A[i];
        }
        
        int lastBit = xor - (xor & (xor - 1));
        // int lastBit = xor & (-xor); // 两句一样的作用，只保留xor的最后一个1。
        int group0 = 0, group1 = 0;
        for (int i = 0; i < A.length; i++) {
            if ((lastBit & A[i]) == 0) {
                group0 ^= A[i];
            } else {
                group1 ^= A[i];
            }
        }
        
        ArrayList<Integer> result = new ArrayList<Integer>();
        result.add(group0);
        result.add(group1);
        return result;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)