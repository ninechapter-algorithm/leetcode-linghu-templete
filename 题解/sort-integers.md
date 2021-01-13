# 整数排序
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/sort-integers/?utm_source=sc-github-wzz)
 ## 题目描述
 给一组整数，按照升序排序，使用选择排序，冒泡排序，插入排序或者任何 O(n<sup>2</sup>) 的排序算法。

 ### 样例说明
 ```
样例  1:
	输入:  [3, 2, 1, 4, 5]
	输出:  [1, 2, 3, 4, 5]
	
	样例解释: 
	返回排序后的数组。

样例 2:
	输入:  [1, 1, 2, 1, 1]
	输出:  [1, 1, 1, 1, 2]
	
	样例解释: 
	返回排好序的数组。

```
 ### 参考代码
 几种$O(n^2)$时间复杂度的排序算法。
```java
//选择排序
public class Solution {
    /*
     * @param A: an integer array
     * @return: 
     */
    public void sortIntegers(int[] A) {
        // write your code here
        for (int i = 0; i < A.length; i++) {
            int minIdx = i;
            for (int j = i; j < A.length; j++) {
                if (A[j] < A[minIdx]) {
                    minIdx = j;
                }
            }
            int tmp = A[i];
            A[i] = A[minIdx];
            A[minIdx] = tmp;
        }
    }
}


//选择排序2
public class Solution {
    /*
     * @param A: an integer array
     * @return: 
     */
    public void sortIntegers(int[] A) {
        // write your code here
        for (int i = 0; i < A.length; i++) {
            for (int j = i + 1; j < A.length; j++) {
                if (A[i] > A[j]) {
                    int tmp = A[i];
                    A[i] = A[j];
                    A[j] = tmp;
                }
            }
        }
    }
}

//插入排序
public class Solution {
    /*
     * @param A: an integer array
     * @return: 
     */
    public void sortIntegers(int[] A) {
        // write your code here
        for (int i = 0; i < A.length; i++) {
            int newVal = A[i];
            int j = i - 1;

            while (j >= 0 && A[j] > newVal) {
                A[j + 1] = A[j];
                j--;
            }
            A[j + 1] = newVal;
        }
    }
}

//冒泡排序
public class Solution {
    /*
     * @param A: an integer array
     * @return: 
     */
    public void sortIntegers(int[] A) {
        // write your code here
        while (true) {
            boolean exchange = false;
            for (int i = 0; i < A.length - 1; i++) {
                if (A[i] > A[i + 1]) {
                    int tmp = A[i];
                    A[i] = A[i + 1];
                    A[i + 1] = tmp;
                    exchange = true;
                }
            }
            if (!exchange) {
                break;
            }
        }
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)