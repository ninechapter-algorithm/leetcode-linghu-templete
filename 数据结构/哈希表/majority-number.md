# 主元素
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/majority-number/?utm_source=sc-github-wzz)
 ## 题目描述
 <p>给定一个整型数组，找出主元素，它在数组中的出现次数严格大于数组元素个数的二分之一。</p><p><br></p>
 ### 样例说明
 
 ### 参考代码
 <p>&nbsp;&nbsp;&nbsp;&nbsp;<br></p>
```java
public class Solution {
    /**
     * @param nums: a list of integers
     * @return: find a  majority number
     */
    public int majorityNumber(ArrayList<Integer> nums) {
        //由于主元素在数组中个数严格大于1/2，所以假设当前元素就是主元素，用count记录当前元素个数与其他元素个数的差值，
        //candidate记录当前元素是什么，最后count一定为正数并且candidate就是主元素
        int count = 0, candidate = -1;
        for (int i = 0; i < nums.size(); i++) {
            if (count == 0) {
                candidate = nums.get(i);
                count = 1;
            } else if (candidate == nums.get(i)) {
                count++;
            } else {
                count--;
            }
        }
        return candidate;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)