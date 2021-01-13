# 最大数
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/largest-number/?utm_source=sc-github-wzz)
 ## 题目描述
 给出一组非负整数，重新排列他们的顺序把他们组成一个最大的整数。
 ### 样例说明
 **样例 1:**
```
输入:[1, 20, 23, 4, 8]
输出:"8423201"
```
**样例 2:**
```
输入:[4, 6, 65]
输出:"6654"
```

 ### 参考代码
 ```java
class NumbersComparator implements Comparator<String> {
	@Override
	public int compare(String s1, String s2) {
		return (s2 + s1).compareTo(s1 + s2);
	}
}

public class Solution {
    
    public String largestNumber(int[] nums) {
        String[] strs = new String[nums.length];
        for (int i = 0; i < nums.length; i++) {
            strs[i] = Integer.toString(nums[i]);
        }
        Arrays.sort(strs, new NumbersComparator());
        StringBuilder sb = new StringBuilder();
        for (int i = 0; i < strs.length; i++) {
            sb.append(strs[i]);
        }
        String result = sb.toString();
        int index = 0;
        while (index < result.length() && result.charAt(index) == '0') {
            index++;
        }
        if (index == result.length()) {
            return "0";
        }
        return result.substring(index);
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)