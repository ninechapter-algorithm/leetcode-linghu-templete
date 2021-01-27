# 数字组合
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/combination-sum/?utm_source=sc-github-wzz)
 ## 题目描述
 给定一个候选数字的集合 `candidates` 和一个目标值 `target`. 找到 `candidates` 中所有的和为 `target` 的组合.

在同一个组合中, `candidates` 中的某个数字不限次数地出现.
 ### 样例说明
 **样例 1:**

```
输入: candidates = [2, 3, 6, 7], target = 7
输出: [[7], [2, 2, 3]]
```

**样例 2:**

```
输入: candidates = [1], target = 3
输出: [[1, 1, 1]]
```
 ### 参考代码
 ```java
// version 1: Remove duplicates & generate a new array
public class Solution {
    /**
     * @param candidates: A list of integers
     * @param target:An integer
     * @return: A list of lists of integers
     */
    public List<List<Integer>> combinationSum(int[] candidates, int target) {
        List<List<Integer>> results = new ArrayList<>();
        if (candidates == null || candidates.length == 0) {
            return results;
        }
        
        int[] nums = removeDuplicates(candidates);
        
        dfs(nums, 0, new ArrayList<Integer>(), target, results);
        
        return results;
    }
    
    private int[] removeDuplicates(int[] candidates) {
        Arrays.sort(candidates);
        
        int index = 0;
        for (int i = 0; i < candidates.length; i++) {
            if (candidates[i] != candidates[index]) {
                candidates[++index] = candidates[i];
            }
        }
        
        int[] nums = new int[index + 1];
        for (int i = 0; i < index + 1; i++) {
            nums[i] = candidates[i];
        }
        
        return nums;
    }
    
    private void dfs(int[] nums,
                     int startIndex,
                     List<Integer> combination,
                     int remainTarget,
                     List<List<Integer>> results) {
        if (remainTarget == 0) {
            results.add(new ArrayList<Integer>(combination));
            return;
        }
        
        for (int i = startIndex; i < nums.length; i++) {
            if (remainTarget < nums[i]) {
                break;
            }
            combination.add(nums[i]);
            dfs(nums, i, combination, remainTarget - nums[i], results);
            combination.remove(combination.size() - 1);
        }
    }
}

// version 2: reuse candidates array
public class Solution {
    public  List<List<Integer>> combinationSum(int[] candidates, int target) {
        List<List<Integer>> result = new ArrayList<>();
        if (candidates == null) {
            return result;
        }

        List<Integer> combination = new ArrayList<>();
        Arrays.sort(candidates);
        helper(candidates, 0, target, combination, result);

        return result;
    }

     void helper(int[] candidates,
                 int index,
                 int target,
                 List<Integer> combination,
                 List<List<Integer>> result) {
        if (target == 0) {
            result.add(new ArrayList<Integer>(combination));
            return;
        }

        for (int i = index; i < candidates.length; i++) {
            if (candidates[i] > target) {
                break;
            }

            if (i != 0 && candidates[i] == candidates[i - 1]) {
                continue;
            }

            combination.add(candidates[i]);
            helper(candidates, i, target - candidates[i], combination, result);
            combination.remove(combination.size() - 1);
        }
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)