# 俄罗斯套娃信封
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/russian-doll-envelopes/?utm_source=sc-github-wzz)
 ## 题目描述
 给一定数量的信封，带有整数对 `(w, h)` 分别代表信封宽度和高度。一个信封的宽高均大于另一个信封时可以放下另一个信封。
求最大的信封嵌套层数。
 ### 样例说明
 **样例 1:**
```
输入：[[5,4],[6,4],[6,7],[2,3]]
输出：3
解释：
最大的信封嵌套层数是 3 ([2,3] => [5,4] => [6,7])。
```

**样例 2:**
```
输入：[[4,5],[4,6],[6,7],[2,3],[1,1]]
输出：4
解释：
最大的信封嵌套层数是 4 ([1,1] => [2,3] => [4,5] / [4,6] => [6,7])。
```
 ### 参考代码
 考点：
* 贪心
* dp

题解：
* 信封存在两个维度，首先贪心按照其中一个维度将信封排序，一个维然后在另度上面寻找最长上升子序列。
* 此处使用二分优化最长上升子序列，在dp数组中二分查找envelope[1]的位置，当envelope[1]超出范围时会返回-（maxlength+1）需要特殊处理，dp[index] = envelope[1]，当返回的位置为最后为len时，说明插入位置为len，则长度可以+1。
```java
public class Solution {
    /**
     * @param envelopes a number of envelopes with widths and heights
     * @return the maximum number of envelopes
     */
    public int maxEnvelopes(int[][] envelopes) {
        // Write your code here
        if(envelopes == null || envelopes.length == 0 
            || envelopes[0] == null || envelopes[0].length != 2)
            return 0;
        Arrays.sort(envelopes, new Comparator<int[]>(){
            public int compare(int[] arr1, int[] arr2){
                if(arr1[0] == arr2[0])
                    return arr2[1] - arr1[1];
                else
                    return arr1[0] - arr2[0];
            } 
        });
        int dp[] = new int[envelopes.length];
        int len = 0;
        for(int[] envelope : envelopes){
            int index = Arrays.binarySearch(dp, 0, len, envelope[1]);
                if(index < 0)
                    index = -index - 1;
            dp[index] = envelope[1];
            if (index == len)
                len++;
        }
        return len;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)