# 升序子序列。
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/increasing-subsequences/?utm_source=sc-github-wzz)
 ## 题目描述
 给定一个整数数组，找到所有不同的可能的升序子序列，一个升序子序列的长度至少应为2。
 ### 样例说明
 例1:
```
输入:
[4,6,7,7]
输出:
[[4,6],[4,6,7],[4,6,7,7],[4,7],[4,7,7],[6,7],[6,7,7],[7,7]]
```

例2:
```
输入:
[65,21,-44,31,-8]
输出:
[[-44,-8],[-44,31],[21,31]]
```

 ### 参考代码
 类似 subsets & subsets II 的做法。
区别在于，对于重复情况的判断要复杂一些。
时间复杂度当然是 $O(n * 2^n)$ 啦
```java
public class Solution {
    /**
     * @param nums: an integer array
     * @return: all the different possible increasing subsequences of the given array
     */
    public List<List<Integer>> findSubsequences(int[] nums) {
        List<List<Integer>> results = new ArrayList<>();
        if (nums == null || nums.length == 0) {
            return results;
        }
        
        boolean[] visited = new boolean[nums.length];
        int[] prev = getPrev(nums);
        dfs(nums, 0, visited, prev, new ArrayList<>(), results);
        
        return results;
    }
    
    private int[] getPrev(int[] nums) {
        Map<Integer, Integer> hash = new HashMap<>();
        int[] prev = new int[nums.length];
        for (int i = 0; i < nums.length; i++) {
            if (hash.containsKey(nums[i])) {
                prev[i] = hash.get(nums[i]);
            } else {
                prev[i] = -1;
            }
            hash.put(nums[i], i);
        }
        
        return prev;
    }
    
    private void dfs(int[] nums,
                     int index,
                     boolean[] visited,
                     int[] prev,
                     List<Integer> subsequence,
                     List<List<Integer>> results) {
        if (subsequence.size() > 1) {
            results.add(new ArrayList<>(subsequence));
        }
                
        for (int i = index; i < nums.length; i++) {
            // if it's non increasing, continue
            if (subsequence.size() > 0 && nums[i] < nums[index - 1]) {
                continue;
            }
            
            // if it's not the first number of the same value after last selected number
            // and the last same value number is not selected, continue
            if (prev[i] != -1 && visited[prev[i]] == false
                    && (subsequence.size() == 0 || index - 1 < prev[i])) {
                continue;
            }
            
            subsequence.add(nums[i]);
            visited[i] = true;
            dfs(nums, i + 1, visited, prev, subsequence, results);
            visited[i] = false;
            subsequence.remove(subsequence.size() - 1);
        }
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)