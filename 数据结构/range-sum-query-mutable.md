# 可变范围求和
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/range-sum-query-mutable/?utm_source=sc-github-wzz)
 ## 题目描述
 给定一个整数数组 `nums`, 然后你需要实现两个函数:

- `update(i, val)` 将数组下标为i的元素修改为val
- `sumRange(l, r)` 返回数组下标在$[l, r]$区间的元素的和
 ### 样例说明
 **样例 1:**

```
输入:
  nums = [1, 3, 5]
  sumRange(0, 2)
  update(1, 2)
  sumRange(0, 2)
输出: 
  9
  8
```

**样例 2:**

```
输入: 
  nums = [0, 9, 5, 7, 3]
  sumRange(4, 4)
  sumRange(2, 4)
  update(4, 5)
  update(1, 7)
  update(0, 8)
  sumRange(1, 2)
输出: 
  3
  15
  12
```
 ### 参考代码
 使用 Binary Indexed Tree（树状数组）
```java
public class NumArray {
    private int[] arr, bit;
    
    /**
     * @return: nothing
     */
    public NumArray(int[] nums) {
        arr = new int[nums.length];
        bit = new int[nums.length + 1];
        
        for (int i = 0; i < nums.length; i++) {
            update(i, nums[i]);
        }
    }
    
    public void update(int index, int val) {
        int delta = val - arr[index];
        arr[index] = val;
        
        for (int i = index + 1; i <= arr.length; i = i + lowbit(i)) {
            bit[i] += delta;
        }
    }
    
    public int getPrefixSum(int index) {
        int sum = 0;
        for (int i = index + 1; i > 0; i = i - lowbit(i)) {
            sum += bit[i];
        }
        return sum;
    }
    
    private int lowbit(int x) {
        return x & (-x);
    }

    public int sumRange(int left, int right) {
        return getPrefixSum(right) - getPrefixSum(left - 1);
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)