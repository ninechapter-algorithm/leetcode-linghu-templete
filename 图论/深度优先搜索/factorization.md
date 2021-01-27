# 因式分解
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/factorization/?utm_source=sc-github-wzz)
 ## 题目描述
 一个非负数可以被视为其因数的乘积。编写一个函数来返回整数 n 的因数所有可能组合。
 ### 样例说明
 **样例1**
```
输入：8
输出： [[2,2,2],[2,4]]
解释： 8 = 2 x 2 x 2 = 2 x 4
```
**样例2**
```
输入：1 
输出： []
```
 ### 参考代码
 使用dfs解决问题。
使用List来保存当前已用因数，进入dfs时在最后一位添加一个因数，从dfs中返回时删除最后一个元素。
当dfs至num=1时，将当前的list存入答案。
```java
public class Solution {
    /**
     * @param n an integer
     * @return a list of combination
     */
    public List<List<Integer>> getFactors(int n) {
        // write your code here
        List<List<Integer>> result = new ArrayList<List<Integer>>();
        helper(result, new ArrayList<Integer>(), n, 2);
        return result;
    }

    public void helper(List<List<Integer>> result, List<Integer> item, int n, int start) {
        if (n <= 1) {
            if (item.size() > 1) {
                result.add(new ArrayList<Integer>(item));
            }
            return;
        }
    
        for (int i = start; i <= Math.sqrt(n); ++i) {
            if (n % i == 0) {
                item.add(i);
                helper(result, item, n / i, i);
                item.remove(item.size()-1);
            }
        } 
        if (n >= start) {
            item.add(n);
            helper(result, item, 1, n);
            item.remove(item.size() - 1);
        }
    }
}

// version: 高频题班
public class Solution {
    /**
     * @param n an integer
     * @return a list of combination
     */

    List<List<Integer>> ans = new ArrayList<>();
    List<Integer> path = new ArrayList<>();

    void dfs(int start, int remain) {
        if (remain == 1) {
            if (path.size() != 1) {
                ans.add(new ArrayList<>(path)); //deep copy
            }
            return;
        }

        for (int i = start; i <= remain; i++) {
            if (i > remain / i) {
                break;
            }
            if (remain % i == 0) {
                path.add(i);                  //进栈
                dfs(i, remain / i);
                path.remove(path.size() - 1); //出栈
            }
        }

        path.add(remain);
        dfs(remain, 1);
        path.remove(path.size() - 1);
    }

    public List<List<Integer>> getFactors(int n) {
        // write your code here
        dfs(2, n);
        return ans;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)