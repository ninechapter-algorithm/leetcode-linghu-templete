# 合并排序数组 II
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/merge-sorted-array-ii/?utm_source=sc-github-wzz)
 ## 题目描述
 <p>合并两个有序升序的整数数组A和B变成一个新的数组。新数组也要有序。</p>
 ### 样例说明
 
 ### 参考代码
 ```cpp
class Solution {
public:
    /**
     * @param A and B: sorted integer array A and B.
     * @return: A new sorted integer array
     */
    vector<int> mergeSortedArray(vector<int> &A, vector<int> &B) {
        vector<int> C;
        int i = 0, j = 0;
        while (i < A.size() && j < B.size()) {
            if (A[i] < B[j]) {
                C.push_back(A[i++]);
            } else {
                C.push_back(B[j++]);
            }
        }
        while (i < A.size()) {
            C.push_back(A[i++]);
        }
        while (j < B.size()) {
            C.push_back(B[j++]);
        }
        return C;
    }
};

```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)