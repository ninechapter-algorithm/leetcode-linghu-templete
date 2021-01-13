# 相同数字
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/same-number/?utm_source=sc-github-wzz)
 ## 题目描述
 给一个数组，如果数组中**存在**相同数字，且至少有两个相同数字的距离小于给定值`k`，输出`YES`，否则输出`NO`。
 ### 样例说明
 **样例1**

```
输入: array = [1,2,3,1,5,9,3] 和 k = 4
输出: "YES"
解释:
index为3的1和index为0的1距离为3，满足题意输出YES。
```

**样例2**

```
输入: array = [1,2,3,5,7,1,5,1,3] 和 k = 4,
输出: "YES"
解释:
index为7的1和index为5的1距离为2，满足题意。
```
 ### 参考代码
 哈希表
```java
public class Solution {
    /**
     * @param nums: the arrays
     * @param k: the distance of the same number
     * @return: the ans of this question
     */
    public String sameNumber(int[] nums, int k) {
        if (nums == null || nums.length == 0) {
            return "NO";
        }
        
        Map<Integer, Integer> position = new HashMap<>();
        for (int i = 0; i < nums.length; i++) {
            if (position.containsKey(nums[i])) {
                if (i - position.get(nums[i]) < k) {
                    return "YES";
                }
            } 
            position.put(nums[i], i);
        }
        
        return "NO";
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)