# 用递归打印数字
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/print-numbers-by-recursion/?utm_source=sc-github-wzz)
 ## 题目描述
 用递归的方法找到从1到最大的N位整数。
 ### 样例说明
 **样例 1:**
```
输入 : N = 1 
输出 :[1,2,3,4,5,6,7,8,9]
```
**样例 2:**
```
输入 : N = 2 
输出 :[[1,2,3,4,5,6,7,8,9,10,11,12,...,99]
```

 ### 参考代码
 ```java
public class Solution {
    /**
     * @param n: An integer.
     * return : An array storing 1 to the largest number with n digits.
     */
    public List<Integer> numbersByRecursion(int n) {
        // write your code here
        ArrayList<Integer> res = new ArrayList<>();
        num(n, 0, res);
        return res;
    }
    
    public void num(int n, int ans,ArrayList<Integer> res){
        
        if(n == 0){
            if(ans > 0){
                res.add(ans);
            }
            return;
        }
        
        int i;
        for(i = 0; i <= 9; i++){
            num(n - 1, ans * 10 + i, res);
        }
        
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)