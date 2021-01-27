# 将数组重新排序以构造最小值
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/reorder-array-to-construct-the-minimum-number/?utm_source=sc-github-wzz)
 ## 题目描述
 给定一个整数数组，请将其重新排序，以构造最小值。
 ### 样例说明
 **样例 1：**
```
输入：[2, 1]
输出：[1, 2]
解释：通过将数组重新排序，可构造 2 个可能性数字：
           1+2=12
           2+1=21
其中，最小值为 12，所以，将数组重新排序后，该数组变为 [1, 2]。
```

**样例 2：**
```
输入：[3, 32, 321]
输出：[321, 32, 3]
解释：通过将数组重新排序，可构造 6 个可能性数字：
	3+32+321=332321
	3+321+32=332132
	32+3+321=323321
	32+321+3=323213
	321+3+32=321332
	321+32+3=321323
其中，最小值为 321323，所以，将数组重新排序后，该数组变为 [321, 32, 3]。
```
 ### 参考代码
 ```java
public class Solution {
    /**
     * @param nums n non-negative integer array
     * @return a string
     */
    public String minNumber(int[] nums) {
        // Write your code here
        int n = nums.length;
        if (n < 1) return "";
        
        String[] strs = new String[n];
        for (int i = 0; i < n; i++) {
            strs[i] = String.valueOf(nums[i]);
        }
        
        Arrays.sort(strs, new Cmp());
        
        String ans = "";
        for (int i = n - 1; i >= 0; i--) {
        	ans = ans.concat(strs[i]);
        }
        
        int i = 0;
        while (i < n && ans.charAt(i) == '0')
            i ++;

        if (i == n) return "0";
        return ans.substring(i);
    }
}
class Cmp implements Comparator<String>{
    @Override
    public int compare(String a, String b) {
        String ab = a.concat(b);
        String ba = b.concat(a);
        return ba.compareTo(ab);
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)