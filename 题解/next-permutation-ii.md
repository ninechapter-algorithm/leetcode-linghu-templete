# 下一个排列
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/next-permutation-ii/?utm_source=sc-github-wzz)
 ## 题目描述
 给定一个若干整数的排列，给出按正数大小进行字典序从小到大排序后的下一个排列。

如果没有下一个排列，则输出字典序最小的序列。
 ### 样例说明
 **样例 1:**
```
输入:1,2,3
输出:1,3,2
```

**样例 2:**
```
输入:3,2,1
输出:1,2,3
```

**样例 3:**
```
输入:1,1,5
输出:1,5,1
```
 ### 参考代码
 ```java
public class Solution {
    /**
     * @param num: an array of integers
     * @return: return nothing (void), do not return anything, modify num in-place instead
     */
     
    public void reverse(int[] num, int start, int end) {
        for (int i = start, j = end; i < j; i++, j--) {
            int temp = num[i];
            num[i] = num[j];
            num[j] = temp;
        }
    }
    
    public void nextPermutation(int[] num) {
        // find the last increase index
        int index = -1;
        for (int i = num.length - 2; i >= 0; i--) {
            if (num[i] < num[i + 1]) {
                index = i;
                break;
            }
        }
        if (index == -1) {
            reverse(num, 0, num.length - 1);
            return;
        }
        
        // find the first bigger one
        int biggerIndex = index + 1;
        for (int i = num.length - 1; i > index; i--) {
            if (num[i] > num[index]) {
                biggerIndex = i;
                break;
            }
        }

        // swap them to make the permutation bigger
        int temp = num[index];
        num[index] = num[biggerIndex];
        num[biggerIndex] = temp;
        
        // reverse the last part
        reverse(num, index + 1, num.length - 1);
    }
}

// 写法二：
public class Solution {
    /**
     * @param nums: A list of integers
     * @return: A list of integers that's next permuation
     */
    public void swapItem(int[] nums, int i, int j) {
    	int temp = nums[i];
		nums[i] = nums[j];
		nums[j] = temp;
	}
	public void swapList(int[] nums, int i, int j) {
		while (i < j) {
			swapItem(nums, i, j);
			i ++; j --;
		}
	}
    public void nextPermutation(int[] nums) {
		int len = nums.length;
		if ( len <= 1)
			return;
		int i = len - 1;
		while (i > 0 && nums[i] <= nums[i - 1]) {
			i --;
		}
		if (i != 0) {
			int j = len - 1;
			while (nums[j] <= nums[i - 1]) j--;
			swapItem(nums, j, i-1);
		}
		swapList(nums, i, len - 1);
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)