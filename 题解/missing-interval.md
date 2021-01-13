# 丢失的间隔
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/missing-interval/?utm_source=sc-github-wzz)
 ## 题目描述
 给定一个排序整数数组，**其中元素的取值范围为[lower，upper] (包括边界)**，返回其缺少的范围。
 ### 样例说明
 
 ### 参考代码
 ```java
public class Solution {
    /**
     * @param nums a sorted integer array
     * @param lower an integer
     * @param upper an integer
     * @return a list of its missing ranges
     */
    public List<String> findMissingRanges(int[] nums, int lower, int upper) {
        // Write your code here
        List<String> results = new ArrayList<String>();
    
        int n = nums.length;
        for (int i = 0; i < n; ++i) {
            if (nums[i] == Integer.MIN_VALUE) {
                lower = nums[i] + 1; 
                continue;
            }
            if (lower == nums[i] - 1) {
                results.add(lower + "");
            } else if (lower < nums[i] - 1) {
                results.add(lower + "->" + (nums[i] - 1));
            }
            if (nums[i] == Integer.MAX_VALUE) {
                return results;
            }
            lower = nums[i] + 1;
        }
        if (lower == upper) {
            results.add(lower + "");
        } else if (lower < upper) {
            results.add(lower + "->" + upper);
        }
        return results;
    }
}

// version: 高频题班
public class Solution {
    /**
     * @param nums  a sorted integer array
     * @param lower an integer
     * @param upper an integer
     * @return a list of its missing ranges
     */

    /*
    public List<String> findMissingRanges(int[] nums, int lower, int upper) {
        // Write your code here
        List<String> ans = new ArrayList<>();

        addRange(ans, lower, nums[0] - 1);

        for (int i = 1; i < nums.length; i++) {
            addRange(ans, nums[i - 1] + 1, nums[i] - 1);
        }
        addRange(ans, nums[nums.length - 1] + 1, upper);

        return ans;
    }

    void addRange(List<String> ans, int st, int ed) {
        if (st > ed) {
            return;
        }
        if (st == ed) {
            ans.add(st + "");
            return;
        }
        ans.add(st + "->" + ed);
    }*/

    
    public List<String> findMissingRanges(int[] nums, int lower, int upper) {
        // Write your code here
        List<String> ans = new ArrayList<>();
        if (nums.length == 0) {
            addRange(ans, lower, upper);
            return ans;
        }

        addRange(ans, lower, (long) nums[0] - 1);

        for (int i = 1; i < nums.length; i++) {
            addRange(ans, (long) nums[i - 1] + 1, (long) nums[i] - 1);
        }
        addRange(ans, (long) nums[nums.length - 1] + 1, upper);

        return ans;
    }

    void addRange(List<String> ans, long st, long ed) {
        if (st > ed) {
            return;
        }
        if (st == ed) {
            ans.add(st + "");
            return;
        }
        ans.add(st + "->" + ed);
    }
    
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)