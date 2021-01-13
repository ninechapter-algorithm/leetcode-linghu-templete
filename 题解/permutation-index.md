# 排列序号
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/permutation-index/?utm_source=sc-github-wzz)
 ## 题目描述
 给出一个不含重复数字的排列，求这些数字的所有排列按字典序排序后该排列的编号。其中，编号从1开始。
 ### 样例说明
 **样例 1:**
```
输入:[1,2,4]
输出:1
```

**样例 2:**
```
输入:[3,2,1]
输出:6
```
 ### 参考代码
 ```java
public class Solution {
	/**
	 * @param A an integer array
	 * @return a long integer
	 */
	long fac(int numerator) {
		long now = 1;
		for (int i = 1; i <= numerator; i++) {
			now *= (long) i;
		}
		return now;
	}

	long generateNum(HashMap<Integer, Integer> hash) {
		long denominator = 1;
		int sum = 0;
		for (int val : hash.values()) {
			if(val == 0 )	
				continue;
			denominator *= fac(val);
			sum += val;
		}
		if(sum==0) {
			return sum;
		}
		return fac(sum) / denominator;
	}

	public long permutationIndex(int[] A) {
		HashMap<Integer, Integer> hash = new HashMap<Integer, Integer>();
		for (int i = 0; i < A.length; i++) {
			if (hash.containsKey(A[i]))
				hash.put(A[i], hash.get(A[i]) + 1);
			else {
				hash.put(A[i], 1);
			}
		}
		long ans = 0;
		for (int i = 0; i < A.length; i++) {
			for (int j = i + 1; j < A.length; j++) {
				if (A[j] < A[i]) {
					hash.put(A[j], hash.get(A[j]) - 1);
					ans += generateNum(hash);
					hash.put(A[j], hash.get(A[j]) + 1);
				}
			}
			hash.put(A[i], hash.get(A[i])-1);
		}
		return ans+1;
	}
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)