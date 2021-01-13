# 生成给定大小的数组
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/generate-arraylist-with-given-size/?utm_source=sc-github-wzz)
 ## 题目描述
 给你一个大小size,生成一个元素`从1 到 size`的数组
 ### 样例说明
 ```
样例 1:
	输入:  size = 4
	输出: [1, 2, 3, 4]
	
	样例解释: 
	 返回一个顺序填充1到4的数组。
	 
样例 2:
	输入:  size = 1
	输出: [1]
	
	样例解释: 
	返回一个顺序填充1到1的数组
	
```

 ### 参考代码
 基本模拟
```java
public class Solution {
    /**
     * @param size an integer
     * @return an array list
     */
    public ArrayList<Integer> generate(int size) {
        // Write your code here
        ArrayList<Integer> result = new ArrayList<Integer>();
        for (int i = 1; i <= size; ++i)
            result.add(i);
        return result;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)