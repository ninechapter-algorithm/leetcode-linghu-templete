# 网址分析
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/url-parser/?utm_source=sc-github-wzz)
 ## 题目描述
 分析一段html语言中的网址
 ### 样例说明
 **样例 1:**

```
输入:
  <html>
    <body>
      <div>
        <a href="http://www.google.com" class="text-lg">Google</a>
        <a href="http://www.facebook.com" style="display:none">Facebook</a>
      </div>
      <div>
        <a href="https://www.linkedin.com">Linkedin</a>
        <a href = "http://github.io">LintCode</a>
      </div>
    </body>
  </html>
输出: 
  [
    "http://www.google.com",
    "http://www.facebook.com",
    "https://www.linkedin.com",
    "http://github.io"
  ]
```

**样例 2:**

```
输入: 
  <html>
    <body>
      <div>
        <a  HREF =    "http://www.google.com" class="text-lg">Google</a>
        <a  HREF = "http://www.facebook.com" style="display:none">Facebook</a>
      </div>
      <div>
        <a href="https://www.linkedin.com">Linkedin</a>
        <a href = "http://github.io">LintCode</a>
      </div>
    </body>
  </html>
输出: 
  [
    "http://github.io",
    "http://www.facebook.com",
    "http://www.google.com",
    "https://www.linkedin.com"
  ]
```
 ### 参考代码
 这是一道字符串处理题目, 你可以手写循环, 遍历字符串, 或者是使用KMP之类的算法查找. 

但是, 正如题目中的提示, 使用正则表达式是高效并且简洁的.

需要查找的是被 `href = ""` 的双引号包含的链接, 注意 `href` 不区分大小写, 并且 `=` 前后的空格数量是随意的, 因为这些都是符合 html 语法的.

另外两点: 确保你查找到的不是空串, 确保你查找到的不是 #.
```java
import java.util.regex.Matcher;
import java.util.regex.Pattern;


public class HtmlParser {
    private static final String HTML_HREF_TAG_PATTERN =  "\\s*(?i)href\\s*=\\s*(\"|')+([^\"'>\\s]*)";
    /**
     * @param content source code
     * @return a list of links
     */
    public List<String> parseUrls(String content) {
        List<String> links = new ArrayList<String>();
        Pattern pattern = Pattern.compile(HTML_HREF_TAG_PATTERN, Pattern.CASE_INSENSITIVE);
        Matcher matcher = pattern.matcher(content);
        String url = null;
        while (matcher.find()) {
            url = matcher.group(2);
            if (url.length() == 0 || url.startsWith("#"))
                continue;
            links.add(url);
        }
        return links;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)