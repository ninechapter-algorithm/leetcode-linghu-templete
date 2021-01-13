# 去除重复元素
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/remove-duplicate-numbers-in-array/?utm_source=sc-github-wzz)
 ## 题目描述
 给一个整数数组，去除重复的元素。

你应该做这些事

1.在原数组上操作
2.将去除重复之后的元素放在数组的开头
3.返回去除重复元素之后的元素个数
 ### 样例说明
 
例1:
```
输入:
nums = [1,3,1,4,4,2]
输出:
[1,3,4,2,?,?]
4

解释:
1. 将重复的整数移动到 nums 的尾部 => nums = [1,3,4,2,?,?].
2. 返回 nums 中唯一整数的数量  => 4.
事实上我们并不关心你把什么放在了 ? 处, 只关心没有重复整数的部分.
```


例2:
```
输入:
nums = [1,2,3]
输出:
[1,2,3]
3
```

 ### 参考代码
 建立一个指针，指针指向目前位置不同的数的末尾，如果当前元素与末尾不同，则加入到末尾
```java
// O(n) time, O(n) space
public class Solution {
    /**
     * @param nums an array of integers
     * @return the number of unique integers
     */
    public int deduplication(int[] nums) {
        // Write your code here
        Set<Integer> set = new HashSet<Integer>();        
        for (int i = 0; i < nums.length; ++i){
            set.add(nums[i]);
        }            
        int result = 0;
        for (Integer i : set){
            nums[result++] = i;
        }    
        return result;
    }
}

// O(nlogn) time, O(1) extra space
public class Solution {
    /**
     * @param nums an array of integers
     * @return the number of unique integers
     */
    public int deduplication(int[] nums) {
        if (nums.length == 0) {
            return 0;
        }
        
        Arrays.sort(nums);
        int len = 0;
        for (int i = 0; i < nums.length; i++) {
            if (nums[i] != nums[len]) {
                nums[++len] = nums[i];
            }
        }
        return len + 1;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)