# 短网址 II
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/tiny-url-ii/?utm_source=sc-github-wzz)
 ## 题目描述
 实现一个顾客短网址，使得顾客可以创立他们自己的短网址. 也就是说, 你需要在 [232. 短网址](https://www.lintcode.com/problem/tiny-url/description) 的基础上再实现一个 `createCustom`.

你需要实现三个方法：
 
* `longToShort(url)` 把一个长网址转换成一个以`http://tiny.url/`开头的短网址
* `shortToLong(url)` 把一个短网址转换成一个长网址
* `createCustom(url, key)` 设定一个长网址的短网址为 `http://tiny.url/` + `key`

你可以任意设计算法，评测只关心：

1. `longToShort` 生成的短网址的key的长度应该等于6 （不算域名和反斜杠）。 可以使用的字符只有 `[a-zA-Z0-9]`. 比如: `abcD9E`
2. 任意两个长的url不会对应成同一个短url，反之亦然。
3. 如果 `createCustom` 不能完成用户期望的设定, 那么应该返回 `"error"`, 反之如果成功将长网址与短网址对应, 应该返回这个短网址.
 ### 样例说明
 **样例 1:**

```
输入:
  createCustom("http://www.lintcode.com/", "lccode")
  shortToLong("http://tiny.url/lccode")
  createCustom("http://www.lintcode.com/", "ltcode")
输出: 
  "http://tiny.url/lccode"
  "http://www.lintcode.com/"
  "error"
```

**样例 2:**

```
输入: 
  longToShort("http://www.lintcode.com/")
  createCustom("http://www.lintcode.com/", "ltcode")
输出: 
  "http://tiny.url/abcdef"      => 该答案不唯一
  "error"
解释: 
  虽然这几乎不可能发生: 
  如果你的 longToShort() 恰好返回了 "http://tiny.url/ltcode",
  那么你的 createCustom() 需要返回 "http://tiny.url/ltcode".
```
 ### 参考代码
 同 [短网址](https://www.lintcode.com/problem/tiny-url/description) 一样, 我们可以用两个哈希表处理长网址和短网址之间的相互映射关系.

我们需要额外处理的便是用户设定的网址与已有的冲突时, 需要返回 "error". 

但是注意这个细节: 如果用户设定的和已有的恰好相同, 那么同样应该返回短网址.
```python
class TinyUrl2:
    def __init__(self):
        self.l2s = {}
        self.s2l = {}
        self.cnt = 0
        self.tinyUrl = 'http://tiny.url/'
        self.charset = 'qwertyuiopasdfghjklzxcvbnm1234567890QWERTYUIOPASDFGHJKLZXCVBNM'
    
    def newShortUrl(self):
        res = ''
        tmp = self.cnt
        for i in range(6):
            res += self.charset[tmp % 62]
            tmp //= 62
        self.cnt += 1
        return self.tinyUrl + res
        
    """
    @param: long_url: a long url
    @param: key: a short key
    @return: a short url starts with http://tiny.url/
    """
    def createCustom(self, long_url, key):
        short_url = self.tinyUrl + key
        if long_url in self.l2s:
            if self.l2s[long_url] == short_url:
                return short_url
            else:
                return 'error' 
        if short_url in self.s2l:
            return 'error'
        self.l2s[long_url] = short_url
        self.s2l[short_url] = long_url
        return short_url

    """
    @param: long_url: a long url
    @return: a short url starts with http://tiny.url/
    """
    def longToShort(self, long_url):
        if long_url in self.l2s:
            return self.l2s[long_url]
        short_url = self.newShortUrl()
        self.l2s[long_url] = short_url
        self.s2l[short_url] = long_url
        return short_url

    """
    @param: short_url: a short url starts with http://tiny.url/
    @return: a long url
    """
    def shortToLong(self, short_url):
        if short_url in self.s2l:
            return self.s2l[short_url]
        else:
            return 'error'
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)