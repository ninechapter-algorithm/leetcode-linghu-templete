# Fizz Buzz 问题
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/fizz-buzz/?utm_source=sc-github-wzz)
 ## 题目描述
 给你一个整数*n*. 从 *1* 到 *n* 按照下面的规则打印每个数：

- 如果这个数被3整除，打印`fizz`.
- 如果这个数被5整除，打印`buzz`.
- 如果这个数能同时被`3`和`5`整除，打印`fizz buzz`.
- 如果这个数既不能被 `3` 整除也不能被 `5` 整除，打印数字`本身。`
 ### 样例说明
 比如 *n* = `15`, 返回一个字符串数组：

```
[
  "1", "2", "fizz",
  "4", "buzz", "fizz",
  "7", "8", "fizz",
  "buzz", "11", "fizz",
  "13", "14", "fizz buzz"
]
```
 ### 参考代码
 有的面试官会要求你能不能只用一个 if 语句来完成这个题，这是一个参考。突破点在于：那我可以用 while 呀~
```java
class Solution {
    /**
     * param n: As description.
     * return: A list of strings.
     */
    public ArrayList<String> fizzBuzz(int n) {
        ArrayList<String> results = new ArrayList<String>();
        int i = 1;
        //p3表示3的多少倍，p5表示5的多少倍
        int p3 = 1, p5 = 1;
        
        while (i <= n) {
          while (i < p3 * 3 && i < p5 * 5) {
            results.add(i + "");
            i++;
          }
        
          if (i <= n && p3 * 3 == p5 * 5) {
            results.add("fizz buzz");
            p3++;
            p5++;
            i++;
            continue;
          }
        
          while (i <= n && p3 * 3 <= i) {
            results.add("fizz");
            p3++;
            i++;
          }
        
          while (i <= n && p5 * 5 <= i) {
            results.add("buzz");
            p5++;
            i++;
          }
        }
        
        return results;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)