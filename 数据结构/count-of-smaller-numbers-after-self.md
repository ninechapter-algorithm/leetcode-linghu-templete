# 比自己小的元素个数
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/count-of-smaller-numbers-after-self/?utm_source=sc-github-wzz)
 ## 题目描述
 给定一个整数数组`nums`，返回一个新的`counts`数组。counts[i]表示：nums[i]右侧比它小的数的个数。
 ### 样例说明
 **样例1**

```plain
输入: [5, 2, 6, 1]
输出: [2, 1, 1, 0]
说明:
5的右侧有2个元素比它小 (2 and 1).
2的右侧有1个元素比它小 (1).
6的右侧有1个元素比它小 (1).
1的右侧有0个元素比它小.
```

**样例2**

```plain
输入: [1, 2, 3, 4]
输出: [0, 0, 0, 0]
```


 ### 参考代码
 真正的 $nlogn$ 的算法
首先使用离散化将原来的数组变为对应的 order 数组。这样就不会有负数，也不会有特别大的数。
如：`[1, 1000, -100, 10, 100]`，将每个数替换为在整个数组中对应的排序。如，1是从小到大第2个，那么就替换为 2。
替换之后得到数组 `[2, 5, 1, 3, 4]`。

接着在用 Binary Indexed Tree 来统计每个数右边有多少个数比他小，只需要从右到左遍历这个数组，一边把数丢到 BIT 里一边计算就行了。
```java
public class Solution {
    /**
     * @param nums: a list of integers
     * @return: return a list of integers
     */
    public List<Integer> countSmaller(int[] nums) {
        if (nums == null || nums.length == 0) {
            return new ArrayList<Integer>();
        }
        
        discretization(nums);

        // build bit array
        int[] bit = new int[nums.length + 1];
        int[] count = new int[nums.length];
        
        for (int i = nums.length - 1; i >= 0; i--) {
            count[i] = getSum(bit, nums[i] - 1);
            update(bit, nums[i]);
        }
        
        List<Integer> result = new ArrayList<Integer>();
        for (int i = 0; i < count.length; i++) {
            result.add(count[i]);
        }
        
        return result;
    }
    
    // this is nlogn
    // sort the orignal array and mapping the number to 
    // the order in the sorted array;
    private void discretization(int[] nums) {
        int[] sorted = nums.clone();
        Arrays.sort(sorted);
        
        for (int i = 0; i < nums.length; i++) {
            nums[i] = Arrays.binarySearch(sorted, nums[i]) + 1;
        }
    }
    
    private void update(int[] bit, int index) {
        for (int i = index; i < bit.length; i = i + lowbit(i)) {
            bit[i]++;
        }
    }
    
    private int getSum(int[] bit, int index) {
        int sum = 0;
        for (int i = index; i > 0; i = i - lowbit(i)) {
            sum += bit[i];
        }
        return sum;
    }
    
    private int lowbit(int x) {
        return x & (-x);
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)