# 计数型布隆过滤器
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/counting-bloom-filter/?utm_source=sc-github-wzz)
 ## 题目描述
 实现一个计数型布隆过滤器, 支持以下方法:
`add(string)`. 往布隆过滤器中加入一个字符串.
`contains(string)`. 检查一个字符串是否在布隆过滤器中.
`remove(string)`. 从布隆计数器中删除一个字符串.
 ### 样例说明
 **样例1**

```
输入:
CountingBloomFilter(3)
add("lint")
add("code")
contains("lint") 
remove("lint")
contains("lint") 

输出: 
[true,false]
```

**样例2**

```
输入:
CountingBloomFilter(3)
add("lint")
add("lint")
contains("lint")
remove("lint")
contains("lint")

输出: 
[true,true]
```
 ### 参考代码
 用map维护数字出现的次数
当加入一个元素时，让map对应改元素的值+1，删除元素时，让map对应该元素的值-1
```cpp
class HashFunction {
private:
    int cap, seed;
public:
    HashFunction(int cap, int seed) {
        this->cap = cap;
        this->seed = seed;
    }

    int hash(string& value) {
        int ret = 0;
        int n = value.size();
        for (int i = 0; i < n; ++i) {
            ret += seed * ret + value[i];
            ret %= cap;
        }
        return ret;
    }
};


class CountingBloomFilter {
private:
    int k;
    vector<HashFunction*> hashFunc;
    vector<int> bits;

public:
    CountingBloomFilter(int k) {
        // initialize your data structure here
        this->k = k;
        for (int i = 0; i < k; ++i)
            hashFunc.push_back(new HashFunction(100000 + i, 2 * i + 3));

        bits.resize(100000 + k, 0);
    }

    void add(string& word) {
        // Write your code here
        for (int i = 0; i < k; ++i) {
            int position = hashFunc[i]->hash(word);
            bits[position] += 1;
        }
    }

    void remove(string& word) {
        // Write your code here
        for (int i = 0; i < k; ++i) {
            int position = hashFunc[i]->hash(word);
            bits[position] -= 1;
        }
    }
    bool contains(string& word) {
        // Write your code here
        for (int i = 0; i < k; ++i) {
            int position = hashFunc[i]->hash(word);
            if (bits[position] <= 0)
                return false;
        }
        return true;
    }
};
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)