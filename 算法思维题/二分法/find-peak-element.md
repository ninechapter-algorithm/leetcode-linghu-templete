# 寻找峰值
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/find-peak-element/?utm_source=sc-github-wzz)
 ## 题目描述
 你给出一个整数数组(size为n)，其具有以下特点：

- 相邻位置的数字是不同的
- A[0] < A[1] 并且 A[n - 2] > A[n - 1]

假定*P*是峰值的位置则满足`A[P] > A[P-1]`且`A[P] > A[P+1]`，返回数组中任意一个峰值的位置。
 ### 样例说明
 ```
样例 1:
	输入:  [1, 2, 1, 3, 4, 5, 7, 6]
	输出:  1 or 6
	
	解释:
	返回峰顶元素的下标


样例 2:
	输入: [1,2,3,4,1]
	输出:  3

```
 ### 参考代码
 这个题 LintCode 和 LeetCode 的 find peak element 是有区别的。
数据上，LintCode 保证数据第一个数比第二个数小，倒数第一个数比到倒数第二个数小。
因此 start, end 的范围要取 1, A.length - 2

二分法。
每次取中间元素，如果大于左右，则这就是peek。
否则取大的一边，两个都大，可以随便取一边。最终会找到peek。

正确性证明：
1. A[0] < A[1] && A[n-2] > A[n-1] 所以一定存在一个peek元素。
2. 二分时，选择大的一边, 则留下的部分仍然满足1 的条件，即最两边的元素都小于相邻的元素。所以仍然必然存在peek。
3. 二分至区间足够小，长度为3, 则中间元素就是peek。
```
[[java]]
class Solution {
    /**
     * @param A: An integers array.
     * @return: return any of peek positions.
     */
    public int findPeak(int[] A) {
        // 1.答案在之间，2.不会出界 
        int start = 1, end = A.length - 2;
        while (start + 1 <  end) {
            int mid = start + (end - start) / 2;
            if (A[mid] < A[mid - 1]) {
                end = mid;
            } else if (A[mid] < A[mid + 1]) {
                start = mid;
            } else {
                return mid;
            }
        }
        if (A[start] < A[end]) {
            return end;
        } else { 
            return start;
        }
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)