# 排列序号II
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/permutation-index-ii/?utm_source=sc-github-wzz)
 ## 题目描述
 <p>给出一个可能包含重复数字的排列，求这些数字的所有排列按字典序排序后该排列在其中的编号。编号从1开始。</p>
 ### 样例说明
 **样例 1:**
```
输入:[1,4,2,2]
输出:3
```

**样例 2:**
```
输入 :[1,6,5,3,1]
输出:24
```

 ### 参考代码
 ```java
// version 1
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

    public long permutationIndexII(int[] A) {
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
            HashMap<Integer, Integer> flag = new HashMap<Integer, Integer>(); 

            for (int j = i + 1; j < A.length; j++) {
                if (A[j] < A[i] && !flag.containsKey(A[j])) {
                    flag.put(A[j], 1);
                    hash.put(A[j], hash.get(A[j])-1);
                    ans += generateNum(hash);
                    hash.put(A[j], hash.get(A[j])+1);
                }

            }
            hash.put(A[i], hash.get(A[i])-1);
        }
        return ans + 1;
    }
}


// version 2
public class Solution {
    /**
     * @param A an integer array
     * @return a long integer
     */
    public long permutationIndexII(int[] A) {
        if (A == null || A.length == 0)
            return 0L;

        Map<Integer, Integer> counter = new HashMap<Integer, Integer>();
        long index = 1, fact = 1, multiFact = 1;
        for (int i = A.length - 1; i >= 0; i--) {
            if (counter.containsKey(A[i])) {
                counter.put(A[i], counter.get(A[i]) + 1);
                multiFact *= counter.get(A[i]);
            } else {
                counter.put(A[i], 1);
            }

            int rank = 0;
            for (int j = i + 1; j < A.length; j++) {
                if (A[i] > A[j]) rank++;
            }

            index += rank * fact / multiFact;
            fact *= (A.length - i);
        }

        return index;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)