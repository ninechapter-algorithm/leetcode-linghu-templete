# 根据身高重排队列
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/queue-reconstruction-by-height/?utm_source=sc-github-wzz)
 ## 题目描述
 假设你有一个顺序被随机打乱的列表，代表了站成一列的人群。每个人被表示成一个二元组`(h, k)`，其中`h`表示他的身高，`k`表示站在他之前的身高高于或等于`h`的人数。你需要将这个队列重新排列以恢复其原有的顺序。
 ### 样例说明
 **样例1**
```
输入：
[[7,0], [4,4], [7,1], [5,0], [6,1], [5,2]]
输出：
[[5,0], [7,0], [5,2], [6,1], [4,4], [7,1]]
```
**样例2**
```
输入：
[[2,0],[1,1]]
输出：
[[2,0],[1,1]]
```

 ### 参考代码
 贪心。
将身高从高到低排序后依次插入即可。对于某个人[h,k]来说，插入答案的第k位。
```java
public class Solution {
    public int[][] reconstructQueue(int[][] people) {
        Arrays.sort(people, (new Comparator<int[]>() {
            @Override
            public int compare(int[] o1, int[] o2) {
                if (o1[0] == o2[0]) {
                    return o1[1] - o2[1];
                } else {
                    return o2[0] - o1[0];
                }
            }
        }));
        List<int[]> resultList = new LinkedList<>();
        for(int[] cur : people){
            resultList.add(cur[1], cur);
        }
        return resultList.toArray(new int[people.length][]);
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)