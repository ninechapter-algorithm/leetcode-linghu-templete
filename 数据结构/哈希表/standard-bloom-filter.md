# 标准型布隆过滤器
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/standard-bloom-filter/?utm_source=sc-github-wzz)
 ## 题目描述
 实现一个标准型布隆过滤器, 支持一下方法:

1. `StandardBloomFilter(k)` 构造方法, 你需要创建k个hash方法
2. `add(string)` 往布隆过滤器中加入一个字符串.
3. `contains(string)` 检查字符串是否在过滤器中
 ### 样例说明
 **样例1**

```
输入:
    StandardBloomFilter(3)
    add("lint")
    add("code")
    contains("lint")
    contains("world")
输出: [true]
```

**样例2**

```
输入:
    StandardBloomFilter(10)
    add("hello")
    contains("hell")
    contains("helloa")
    contains("hello")
    contains("hell")
    contains("helloa")
    contains("hello")
输出: [false,false,true,false,false,true]
```
 ### 参考代码
 利用哈希表进行维护，维护某个值是否出现过
当加入一个数时，在哈希表里记录下
当删除一个数时，从哈希表里将这个数删掉即可
```java
import java.util.BitSet;

class HashFunction {
    public int cap, seed;

    public HashFunction(int cap, int seed) {
        this.cap = cap;
        this.seed = seed;
    }

    public int hash(String value) {
        int ret = 0;
        int n = value.length();
        for (int i = 0; i < n; ++i) {
            ret += seed * ret + value.charAt(i);
            ret %= cap;
        }
        return ret;
    }
}

public class StandardBloomFilter {

    public BitSet bits;
    public int k;
    public List<HashFunction> hashFunc;

    public StandardBloomFilter(int k) {
        // initialize your data structure here
        this.k = k;
        hashFunc = new ArrayList<HashFunction>();
        for (int i = 0; i < k; ++i)
            hashFunc.add(new HashFunction(100000 + i, 2 * i + 3));
        bits = new BitSet(100000 + k);
    }

    public void add(String word) {
        // Write your code here
        for (int i = 0; i < k; ++i) {
            int position = hashFunc.get(i).hash(word);
            bits.set(position);
        }
    }

    public boolean contains(String word) {
        // Write your code here
        for (int i = 0; i < k; ++i) {
            int position = hashFunc.get(i).hash(word);
            if (!bits.get(position))
                return false;
        }
        return true;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)