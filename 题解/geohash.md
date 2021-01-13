# Geo哈希
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/geohash/?utm_source=sc-github-wzz)
 ## 题目描述
 Geo哈希是一个著名的哈希算法，用于将坐标哈希成一个32位字符串
[Geohash](https://en.wikipedia.org/wiki/Geohash)
[http://geohash.co/](http:// "http://geohash.co/")
 ### 样例说明
 **样例1**

```
输入: 
lat = 39.92816697 
lng = 116.38954991
precision = 12 
输出: "wx4g0s8q3jf9"
```

**样例2**

```
输入: 
lat = -90
lng = 180
precision = 12 
输出: "pbpbpbpbpbpb"
```

 ### 参考代码
 直接按照链接中的做法进行哈希即可
```python
class GeoHash:
    # @param {double} latitude, longitude a location coordinate pair
    # @param {int} precision an integer between 1 to 12
    # @return {string} a base32 string
    def encode(self, latitude, longitude, precision):
        # Write your code here
        _base32 = "0123456789bcdefghjkmnpqrstuvwxyz"
        lat_bin = self.get_bin(latitude, -90, 90)
        lng_bin = self.get_bin(longitude, -180, 180)
        
        hash_code, b = '', ''
        for i in xrange(30):
            b += lng_bin[i] + lat_bin[i]

        for i in xrange(0, 60, 5):
            hash_code += _base32[int(b[i:i + 5], 2)]

        return hash_code[:precision]
            

    def get_bin(self, value, left, right):
        b = ''
        for i in xrange(30):
            mid = (left + right) / 2.0
            if value > mid:
                left = mid
                b += '1'
            else:
                right = mid
                b += '0'
        return b
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)