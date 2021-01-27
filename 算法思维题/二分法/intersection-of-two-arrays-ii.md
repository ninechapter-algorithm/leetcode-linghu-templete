# 两数组的交集 II
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/intersection-of-two-arrays-ii/?utm_source=sc-github-wzz)
 ## 题目描述
 给定两个数组，计算两个数组的交集
 ### 样例说明
 **样例1**

```
输入: 
nums1 = [1, 2, 2, 1], nums2 = [2, 2]
输出: 
[2, 2]
```

**样例2**

```
输入: 
nums1 = [1, 1, 2], nums2 = [1]
输出: 
[1]
```
 ### 参考代码
 用map维护前一个数组中每个值出现的次数
然后遍历第二个数组，对于每个遍历到的数，在map中将这个数出现的次数-1
```java
public class Solution {
    /**
     * @param nums1 an integer array
     * @param nums2 an integer array
     * @return an integer array
     */
    public int[] intersection(int[] nums1, int[] nums2) {
        // Write your code here
        Map<Integer, Integer> map = new HashMap<Integer, Integer>();
        for(int i = 0; i < nums1.length; ++i) {
            if (map.containsKey(nums1[i]))
                map.put(nums1[i], map.get(nums1[i]) + 1); 
            else
                map.put(nums1[i], 1);
        }

        List<Integer> results = new ArrayList<Integer>();

        for (int i = 0; i < nums2.length; ++i)
            if (map.containsKey(nums2[i]) &&
                map.get(nums2[i]) > 0) {
                results.add(nums2[i]);
                map.put(nums2[i], map.get(nums2[i]) - 1); 
            }

        int result[] = new int[results.size()];
        for(int i = 0; i < results.size(); ++i)
            result[i] = results.get(i);

        return result;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)