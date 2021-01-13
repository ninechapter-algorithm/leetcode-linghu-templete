# 四数之和
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/4sum/?utm_source=sc-github-wzz)
 ## 题目描述
 <p><span style="line-height: 30px;">给一个包含n个数的整数数组S，在S中找到所有使得和为给定整数target的四元组(a, b, c, d)。</span></p>
 ### 样例说明
 例1:
```
输入:[2,7,11,15],3
输出:[]

```

例2:
```
输入:[1,0,-1,0,-2,2],0
输出:
[[-1, 0, 0, 1]
,[-2, -1, 1, 2]
,[-2, 0, 0, 2]]
```


 ### 参考代码
 固定两个点，然后用双指针的做法，扫描一下后续数组，记录答案即可。
```java
public class Solution {
	public List<List<Integer>> fourSum(int[] num, int target) {
		List<List<Integer>> rst = new ArrayList<List<Integer>>();
		Arrays.sort(num);

		for (int i = 0; i < num.length - 3; i++) {
			if (i != 0 && num[i] == num[i - 1]) {
				continue;
			}

			for (int j = i + 1; j < num.length - 2; j++) {
				if (j != i + 1 && num[j] == num[j - 1])
					continue;

				int left = j + 1;
				int right = num.length - 1;
				while (left < right) {
					int sum = num[i] + num[j] + num[left] + num[right];
					if (sum < target) {
						left++;
					} else if (sum > target) {
						right--;
					} else {
						ArrayList<Integer> tmp = new ArrayList<Integer>();
						tmp.add(num[i]);
						tmp.add(num[j]);
						tmp.add(num[left]);
						tmp.add(num[right]);
						rst.add(tmp);
						left++;
						right--;
						while (left < right && num[left] == num[left - 1]) {
							left++;
						}
						while (left < right && num[right] == num[right + 1]) {
							right--;
						}
					}
				}
			}
		}

		return rst;
	}
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)