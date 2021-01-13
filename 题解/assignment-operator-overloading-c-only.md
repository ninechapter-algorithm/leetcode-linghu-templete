# 赋值运算符重载
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/assignment-operator-overloading-c-only/?utm_source=sc-github-wzz)
 ## 题目描述
 实现赋值运算符重载函数，确保：

- 新的数据可准确地被复制
- 旧的数据可准确地删除/释放
- 可进行 `A = B = C` 赋值


 ### 样例说明
 如果进行 `A = B` 赋值，则 A 中的数据被删除，取而代之的是 B 中的数据。

如果进行 `A = B = C` 赋值，则 A 和 B 都复制了 C 中的数据。
 ### 参考代码
 ```cpp
class Solution {
public:
    char *m_pData;
    Solution() {
        this->m_pData = NULL;
    }
    Solution(char *pData) {
        if (pData) {
            m_pData = new char[strlen(pData) + 1];
            strcpy(m_pData, pData);
        } else {
            m_pData = NULL;
        }
    }

    // Implement an assignment operator
    Solution operator=(const Solution &object) {
        if (this == &object) {
            return *this;
        }
        
        if (object.m_pData) {
            char *temp = m_pData;
            try {
                m_pData = new char[strlen(object.m_pData)+1];
                strcpy(m_pData, object.m_pData);
                if (temp)
                    delete[] temp;
            } catch (bad_alloc& e) {
                m_pData = temp;
            }
        } else {
            m_pData = NULL;
        }
        return *this;
    }
};

```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)