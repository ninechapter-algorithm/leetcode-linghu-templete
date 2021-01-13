# 2 Sum
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/2-sum/?utm_source=sc-github-wzz)
 ## 题目描述
 1754
 ### 样例说明
 1754
 ### 参考代码
 ```java
  public class Solution {
    public int[] twoSum(int[] nums, int target) {
      Map<Integer, Integer> hash = new HashMap<Integer, Integer> ();
      int[] result = new int[2];
      for (int i = 0; i < nums.length; ++i) {
        if (hash.containsKey(target - nums[i])) {
          result[0] = hash.get(target - nums[i]) + 1;
          result[1] = i + 1;
          break;
        }
        hash.put(nums[i], i);
      }
      return result;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)