# 余弦相似度
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/cosine-similarity/?utm_source=sc-github-wzz)
 ## 题目描述
 余弦相似性是内积空间的两个矢量之间的相似性的度量，其测量它们之间的角度的余弦。 0° 的余弦为 1，对于任何其他角度，余弦小于 1。

Wiki 链接: [Cosine Similarity](https://en.wikipedia.org/wiki/Cosine_similarity "")

这里给出公式:

![cosine-similarity](https://lintcode-media.s3.amazonaws.com/problem/cosine-similarity.png "")

给你两个相同大小的向量 *A* *B*，求出他们的余弦相似度。

返回 `2.0000` 如果余弦相似不合法 (比如 A = [0] B = [0])。
 ### 样例说明
 **样例 1：**
```
输入：A = [1,4,0], B = [1,2,3]
输出：0.5834
```
**样例 2：**
```
输入：A = [1], B = [2]
输出：1.0000
```
 ### 参考代码
 ```cpp
class Solution {
public:
    /**
     * @param A: An integer array.
     * @param B: An integer array.
     * @return: Cosine similarity.
     */
    double cosineSimilarity(vector<int> A, vector<int> B) {
        int factor = 0;
        for (int i = 0; i < A.size(); i++) {
            factor += A[i] * B[i];
        }

        int sumA = 0;
        for (int i = 0; i < A.size(); i++) {
            sumA += A[i] * A[i];
        }
        int sumB = 0;
        for (int i = 0; i < B.size(); i++) {
            sumB += B[i] * B[i];
        }

        if (sumA == 0 || sumB == 0) {
            return 2;
        }

        return factor / sqrt(sumA) / sqrt(sumB);
    }
};


```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)