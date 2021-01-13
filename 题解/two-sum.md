# 两数之和
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/two-sum/?utm_source=sc-github-wzz)
 ## 题目描述
 给一个整数数组，找到两个数使得他们的和等于一个给定的数 *target*。

你需要实现的函数`twoSum`需要返回这两个数的下标, 并且第一个下标小于第二个下标。注意这里下标的范围是 0 到 *n-1*。

 ### 样例说明
 ```
Example1:
给出 numbers = [2, 7, 11, 15], target = 9, 返回 [0, 1].
Example2:
给出 numbers = [15, 2, 7, 11], target = 9, 返回 [1, 2].
```
 ### 参考代码
 Given an array of integers, find two numbers such that they add up to a specific target number.

The function twoSum should return indices of the two numbers such that they add up to the target, where index1 must be less than index2. Please note that your returned answers (both index1 and index2) are not zero-based.

You may assume that each input would have exactly one solution.

Input: numbers={2, 7, 11, 15}, target=9
Output: index1=1, index2=2
```java
public class Solution {
    /*
     * @param numbers : An array of Integer
     * @param target : target = numbers[index1] + numbers[index2]
     * @return : [index1 + 1, index2 + 1] (index1 < index2)
         numbers=[2, 7, 11, 15],  target=9
         return [1, 2]
     */
    public int[] twoSum(int[] numbers, int target) {
        //用一个hashmap来记录，key记录target-numbers[i]的值，value记录numbers[i]的i的值，如果碰到一个
        //numbers[j]在hashmap中存在，那么说明前面的某个numbers[i]和numbers[j]的和为target，i和j即为答案
        HashMap<Integer,Integer> map = new HashMap<>();

        for (int i = 0; i < numbers.length; i++) {
            if (map.get(numbers[i]) != null) {
                int[] result = {map.get(numbers[i]), i};
                return result;
            }
            map.put(target - numbers[i], i);
        }
        
        int[] result = {};
        return result;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)