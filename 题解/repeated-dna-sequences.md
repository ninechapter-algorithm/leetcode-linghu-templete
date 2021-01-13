# 重复的DNA序列 
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/repeated-dna-sequences/?utm_source=sc-github-wzz)
 ## 题目描述
 所有DNA由一系列缩写为A，C，G和T的核苷酸组成，例如：“ACGAATTCCG”。 在研究DNA时，有时识别DNA中的重复序列是非常必要的。

编写一个函数来查找DNA分子中，长度为10个字母的，不止一次出现的序列（子串）。
 ### 样例说明
 **样例1**

```
输入: "A"
输出: []
```

**样例2**

```
输入: s = "AAAAACCCCCAAAAACCCCCCAAAAAGGGTTT"
输出: ["AAAAACCCCC", "CCCCCAAAAA"]
```
 ### 参考代码
 ```java
public class Solution {
    public int encode(String s) {
        int sum = 0;
        for (int i = 0; i < s.length(); i++) {
            if (s.charAt(i) == 'A') {
                sum = sum * 4;
            } else if (s.charAt(i) == 'C') {
                sum = sum * 4 + 1;
            } else if (s.charAt(i) == 'G') {
                sum = sum * 4 + 2;
            } else {
                sum = sum * 4 + 3;
            }
        }
        return sum;
    }
    public List<String> findRepeatedDnaSequences(String s) {
        HashSet<Integer> hash = new HashSet<Integer>();
        HashSet<String> dna = new HashSet<String>();
        for (int i = 9; i < s.length(); i++) {
            String subString = s.substring(i - 9, i + 1);
            int encoded = encode(subString);
            if (hash.contains(encoded)) {
                dna.add(subString);
            } else {
                hash.add(encoded);
            }
        }
        List<String> result = new ArrayList<String>();
        for (String d: dna) {
            result.add(d);
        }
        return result;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)