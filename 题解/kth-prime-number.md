# 第K个质数
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/kth-prime-number/?utm_source=sc-github-wzz)
 ## 题目描述
 给出质数`n`，输出它是第几个质数。
 ### 样例说明
 **样例1**

```
输入: n = 3
输出: 2
解释:
[2,3,5]，3是第2个质数。
```



**样例2**

```
输入: n = 11
输出: 5
解释:
[2,3,5,7,11]，11是第五个质数。
```
 ### 参考代码
 ```cpp
class Solution {

public:

    /*

     * @param k: The number k.

     * @return: The kth prime number as description.

     */

    long long kthPrimeNumber(int k) {

        priority_queue<long long> heap;

        unordered_map<long long, bool> hash;

        

        long long primes[3];

        primes[0] = 3; primes[1] = 5; primes[2] = 7;

        heap.push(-3); heap.push(-5); heap.push(-7);

        

        for (int i = 0; i < k - 1; i++) {

            long long top = -heap.top();

            heap.pop();

            

            for (int j = 0; j < 3; j++) {

                if (hash.find(top * primes[j]) == hash.end()) {

                    hash[top * primes[j]] = true;

                    heap.push(-top * primes[j]);

                }

            }

        }

        return -heap.top();

    }

};

```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)