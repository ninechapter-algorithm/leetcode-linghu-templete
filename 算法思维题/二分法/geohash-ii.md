# Geo哈希 II
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/geohash-ii/?utm_source=sc-github-wzz)
 ## 题目描述
 这题是 [Geohash](http://www.lintcode.com/problem/geohash/)的加强版
将一个字符串用Geohash的逆运算求出latitude和longitude
Geohash细节见帮助[Geohash](http://www.lintcode.com/zh-cn/help/geohash/)或者wiki [GeoHash](https://en.wikipedia.org/wiki/Geohash)


 ### 样例说明
 **样例1**

```
输入: "wx4g0s"`
输出: lat = 39.92706299 and lng = 116.39465332
```

**样例2**

```
输入: "w"
输出: lat = 22.50000000 and lng = 112.50000000
```

 ### 参考代码
 二分求解
```java
public class GeoHash {
    /**
     * @param geohash a base32 string
     * @return latitude and longitude a location coordinate pair
     */
    public double[] decode(String geohash) {
        // Write your code here
        String _base32 = "0123456789bcdefghjkmnpqrstuvwxyz";
        int[] mask = {16, 8, 4, 2, 1};
        double[] lon = {-180, 180};
        double[] lat = {-90, 90};
        boolean is_even = true;

        for (int i = 0; i < geohash.length(); ++i) {
            int val = _base32.indexOf(geohash.charAt(i));
            for (int j = 0; j < 5; ++j) {
                if (is_even) {
                    refine_interval(lon, val, mask[j]);
                } else {
                    refine_interval(lat, val, mask[j]);
                }
                is_even = ! is_even;
            }
        }
        double[] location = {(lat[0] + lat[1]) / 2.0, (lon[0] + lon[1]) / 2.0};
        return location;
    }

    public void refine_interval(double[] interval, int val, int mask) {
        if ((val & mask) > 0) {
            interval[0] = (interval[0] + interval[1]) / 2.0;
        } else {
            interval[1] = (interval[0] + interval[1]) / 2.0;
        }
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)