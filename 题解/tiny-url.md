# 短网址
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/tiny-url/?utm_source=sc-github-wzz)
 ## 题目描述
 给出一个长网址，返回一个短网址。

你需要实现两个方法：

* `longToShort(url)` 把一个长网址转换成一个以`http://tiny.url/`开头的短网址
* `shortToLong(url)` 把一个短网址转换成一个长网址

你可以任意设计算法，评测只关心两件事：

1. 短网址的key的长度应该等于6 （不算域名和反斜杠）。 可以使用的字符只有 `[a-zA-Z0-9]`. 比如: `abcD9E`
2. 任意两个长的url不会对应成同一个短url，反之亦然。
 ### 样例说明
 **样例 1:**

```
输入: shortToLong(longToShort("http://www.lintcode.com/faq/?id=10"))
输出: "http://www.lintcode.com/faq/?id=10"
解释: 
  longToShort()被调用时你可以返回任何短网址, 比如 "http://tiny.url/abcdef".
  或者 "http://tiny.url/ABCDEF" 也时可以的.
```

**样例 2:**

```
输入: 
  shortToLong(longToShort("http://www.lintcode.com/faq/?id=10"))
  shortToLong(longToShort("http://www.lintcode.com/faq/?id=10"))
输出: 
  "http://www.lintcode.com/faq/?id=10"
  "http://www.lintcode.com/faq/?id=10"
```
 ### 参考代码
 用两个哈希表, 一个是短网址映射到长网址, 一个是长网址映射到短网址.

短网址是固定的格式: "http://tiny.url/" + 6个字符, 字符可以是任意的.

为了避免重复, 我们可以按照字典序依次使用, 或者在随机生成的基础上用一个集合来记录是否使用过.
```java
// version 1: Random
public class TinyUrl {
    private Map<String, String> long2Short;
    private Map<String, String> short2Long;

    public TinyUrl() {
        long2Short = new HashMap<String, String>();
        short2Long = new HashMap<String, String>();
    }

    /**
     * @param url a long url
     * @return a short url starts with http://tiny.url/
     */
    public String longToShort(String url) {
        if (long2Short.containsKey(url)) {
            return long2Short.get(url);
        }

        while (true) {
            String shortURL = generateShortURL();
            if (!short2Long.containsKey(shortURL)) {
                short2Long.put(shortURL, url);
                long2Short.put(url, shortURL);
                return shortURL;
            }
        }
    }

    /**
     * @param url a short url starts with http://tiny.url/
     * @return a long url
     */
    public String shortToLong(String url) {
        if (!short2Long.containsKey(url)) {
            return null;
        }

        return short2Long.get(url);
    }

    private String generateShortURL() {
        String allowedChars = "0123456789" + "abcdefghijklmnopqrstuvwxyz" + "ABCDEFGHIJKLMNOPQRSTUVWXYZ";

        Random rand = new Random();
        String shortURL = "http://tiny.url/";
        for (int i = 0; i < 6; i++) {
            int index = rand.nextInt(62);
            shortURL += allowedChars.charAt(index);
        }

        return shortURL;
    }
}

// version 2: base62
public class TinyUrl {
    public static int GLOBAL_ID = 0;
    private HashMap<Integer, String> id2url = new HashMap<Integer, String>();
    private HashMap<String, Integer> url2id = new HashMap<String, Integer>();

    private String getShortKey(String url) {
        return url.substring("http://tiny.url/".length());
    }

    private int toBase62(char c) {
        if (c >= '0' && c <= '9') {
            return c - '0';
        }
        if (c >= 'a' && c <= 'z') {
            return c - 'a' + 10;
        }
        return c - 'A' + 36;
    }

    private int shortKeytoID(String short_key) {
        int id = 0;
        for (int i = 0; i < short_key.length(); ++i) {
            id = id * 62 + toBase62(short_key.charAt(i));
        }
        return id;
    }

    private String idToShortKey(int id) {
        String chars = "0123456789abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ";
        String short_url = "";
        while (id > 0) {
            short_url = chars.charAt(id % 62) + short_url;
            id = id / 62;
        }
        while (short_url.length() < 6) {
            short_url = "0" + short_url;
        }
        return short_url;
    }

    /**
     * @param url a long url
     * @return a short url starts with http://tiny.url/
     */
    public String longToShort(String url) {
        if (url2id.containsKey(url)) {
            return "http://tiny.url/" + idToShortKey(url2id.get(url));
        }
        GLOBAL_ID++;
        url2id.put(url, GLOBAL_ID);
        id2url.put(GLOBAL_ID, url);
        return "http://tiny.url/" + idToShortKey(GLOBAL_ID);
    }

    /**
     * @param url a short url starts with http://tiny.url/
     * @return a long url
     */
    public String shortToLong(String url) {
        String short_key = getShortKey(url);
        int id = shortKeytoID(short_key);
        return id2url.get(id);
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)