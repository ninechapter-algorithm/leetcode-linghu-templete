# 哈希函数
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/hash-function/?utm_source=sc-github-wzz)
 ## 题目描述
 <p>在数据结构中，哈希函数是用来将一个字符串（或任何其他类型）转化为小于哈希表大小且大于等于零的整数。一个好的哈希函数可以尽可能少地产生冲突。一种广泛使用的哈希函数算法是使用数值33，假设任何字符串都是基于33的一个大整数，比如：</p><p style="color: rgb(113, 113, 113); font-family: 'Open Sans', 'Helvetica Neue', Helvetica, Arial, sans-serif;">hashcode("abcd") = (ascii(a) * 33<span style="position: relative; font-size: 12px; line-height: 0; vertical-align: baseline; top: -0.5em;">3</span>&nbsp;+&nbsp;<span style="line-height: 1.42857143;">ascii(</span><span style="line-height: 1.42857143;">b) * 33</span><span style="position: relative; font-size: 12px; line-height: 0; vertical-align: baseline; top: -0.5em;">2</span><span style="line-height: 1.42857143;">&nbsp;+&nbsp;</span><span style="line-height: 1.42857143;">ascii(</span><span style="line-height: 1.42857143;">c) *33 +&nbsp;</span><span style="line-height: 1.42857143;">ascii(</span><span style="line-height: 1.42857143;">d)) %&nbsp;</span>HASH_SIZE<span style="line-height: 1.42857143;">&nbsp;</span></p><p style="color: rgb(113, 113, 113); font-family: 'Open Sans', 'Helvetica Neue', Helvetica, Arial, sans-serif;"><span style="line-height: 1.42857143;">&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; = (</span><span style="line-height: 1.42857143;">97* 33</span><span style="font-size: 12px; line-height: 0; position: relative; vertical-align: baseline; top: -0.5em;">3</span><span style="line-height: 1.42857143;">&nbsp;</span><span style="line-height: 1.42857143;">+ 98</span><span style="line-height: 1.42857143;">&nbsp;* 33</span><span style="font-size: 12px; line-height: 0; position: relative; vertical-align: baseline; top: -0.5em;">2</span><span style="line-height: 1.42857143;">&nbsp;+ 99</span><span style="line-height: 1.42857143;">&nbsp;* 33 +100</span><span style="line-height: 1.42857143;">) % HASH_SIZE</span></p><p style="color: rgb(113, 113, 113); font-family: 'Open Sans', 'Helvetica Neue', Helvetica, Arial, sans-serif;"><span style="line-height: 1.42857143;">&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; =&nbsp;</span>3595978 % HASH_SIZE</p><p>其中HASH_SIZE表示哈希表的大小(可以假设一个哈希表就是一个索引0 ~ HASH_SIZE-1的数组)。</p><p>给出一个字符串作为key和一个哈希表的大小，返回这个字符串的哈希值。</p>
 ### 样例说明
 **样例 1:**

```
输入:  key = "abcd", size = 1000
输出: 978	
样例解释：(97 * 33^3 + 98*33^2 + 99*33 + 100*1)%1000 = 978
```

**样例 2:**

```
输入:  key = "abcd", size = 100
输出: 78	
样例解释：(97 * 33^3 + 98*33^2 + 99*33 + 100*1)%100 = 78
```
 ### 参考代码
 取模过程要使用同余定理：
(a * b ) % MOD = ((a % MOD) * (b % MOD)) % MOD
```python
class Solution:
    """
    @param key: A String you should hash
    @param HASH_SIZE: An integer
    @return an integer
    """
    def hashCode(self, key, HASH_SIZE):
        # write your code here
        ans = 0
        for x in key:
            ans = (ans * 33 + ord(x)) % HASH_SIZE
        return ans
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)