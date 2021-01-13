# 杨辉三角
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/pascals-triangle/?utm_source=sc-github-wzz)
 ## 题目描述
 给定一个非负整数 *numRows，*生成杨辉三角的前 *numRows* 行。

![图片](https://media-cdn.jiuzhang.com/markdown/images/7/6/60e49d2e-9ffa-11e9-a15b-0242ac110002.jpg)

在杨辉三角中，每个数是它左上方和右上方的数的和。
 ### 样例说明
 **样例 1:**

```
输入: 5
输出:
[
     [1],
    [1,1],
   [1,2,1],
  [1,3,3,1],
 [1,4,6,4,1]
]
```

**样例 2:**

```
输入: 3
输出:
[
     [1],
    [1,1],
   [1,2,1]
]
```


 ### 参考代码
 ```java
class Solution {
    public List<List<Integer>> generate(int numRows) {
        List<List<Integer>> triangle = new ArrayList<List<Integer>>();

        // First base case; if user requests zero rows, they get zero rows.
        if (numRows == 0) {
            return triangle;
        }

        // Second base case; first row is always [1].
        triangle.add(new ArrayList<>());
        triangle.get(0).add(1);

        for (int rowNum = 1; rowNum < numRows; rowNum++) {
            List<Integer> row = new ArrayList<>();
            List<Integer> prevRow = triangle.get(rowNum-1);

            // The first row element is always 1.
            row.add(1);

            // Each triangle element (other than the first and last of each row)
            // is equal to the sum of the elements above-and-to-the-left and
            // above-and-to-the-right.
            for (int j = 1; j < rowNum; j++) {
                row.add(prevRow.get(j-1) + prevRow.get(j));
            }

            // The last row element is always 1.
            row.add(1);

            triangle.add(row);
        }

        return triangle;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)