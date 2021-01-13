# 最长连续序列
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/longest-consecutive-sequence/?utm_source=sc-github-wzz)
 ## 题目描述
 <p>给定一个未排序的整数数组，找出最长连续序列的长度。</p>
 ### 样例说明
 ***样例 1***
```
输入 : [100, 4, 200, 1, 3, 2]
输出 : 4
解释 : 这个最长的连续序列是 [1, 2, 3, 4]. 返回所求长度 4
```
 ### 参考代码
 Given an unsorted array of integers, find the length of the longest consecutive elements sequence.

For example,
Given [100, 4, 200, 1, 3, 2],
The longest consecutive elements sequence is [1, 2, 3, 4]. Return its length: 4.

Your algorithm should run in O(n) complexity.
```java
public class Solution {
    /**
     * @param nums: A list of integers
     * @return an integer
     */
    public int longestConsecutive(int[] nums) {
        HashSet<Integer> set = new HashSet<>();
        for (int i = 0; i < nums.length; i++) {
            set.add(nums[i]);
        }
        
        int longest = 0;
        for (int i = 0; i < nums.length; i++) {
            int down = nums[i] - 1;
            while (set.contains(down)) {
                set.remove(down);
                down--;
            }
            
            int up = nums[i] + 1;
            while (set.contains(up)) {
                set.remove(up);
                up++;
            }
            
            longest = Math.max(longest, up - down - 1);
        }
        
        return longest;
    }
}

// version: 高频题班
public class Solution {
    /**
     * @param nums: A list of integers
     * @return an integer
     */
    public int longestConsecutive(int[] num) {
        // write you code here
        Set<Integer> set = new HashSet<>();
        for (int item : num) {
            set.add(item);
        }

        int ans = 0;
        for (int item : num) {
            if (set.contains(item)) {
                set.remove(item);

                int l = item - 1;
                int r = item + 1;
                while (set.contains(l)) {
                    set.remove(l);
                    l--;
                }
                while (set.contains(r)) {
                    set.remove(r);
                    r++;
                }
                ans = Math.max(ans, r - l - 1);
            }
        }
        return ans;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)