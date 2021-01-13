# 多个数组的交集
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/intersection-of-arrays/?utm_source=sc-github-wzz)
 ## 题目描述
 给出多个数组，求它们的交集。输出他们交集的大小。
 ### 样例说明
 **样例 1:**
```
	输入:  [[1,2,3],[3,4,5],[3,9,10]]
	输出:  1
	
	解释:
	只有3出现在三个数组中。
```
	
**样例 2:**
```
	输入: [[1,2,3,4],[1,2,5,6,7][9,10,1,5,2,3]]
	输出:  2
	
	解释:
	交集是[1,2].
```


 ### 参考代码
 基于 Priority Queue 的版本。
假设每个数组长度为 n, 一共 k 个数组。
时间复杂度为 $O(knlogn + nklogk)$
其中 $knlogn$ 是 k 个数组进行分别排序的时间复杂度
$nklogk$ 是 总共 nk 个数从 PriorityQueue 中进出，每次进出 logk。

相比使用 HashMap 的算法的时间复杂度 $O(nk)$ 这个方法并没有什么时间上的优势。
但是这个方法的空间复杂度很低，只有 $O(k)$，即多少个数组就花费多少的额外空间。

在面试中也是很有可能会被要求不用 HashMap 或者实现一个比 $O(n)$ 更低的空间复杂度的算法。因此这个程序的方法也是需要掌握的。
```java
public class Solution {
    class Pair {
        public int row, col;
        
        public Pair(int row, int col) {
            this.row = row;
            this.col = col;
        }
    }
    
    /**
     * @param arrs: the arrays
     * @return: the number of the intersection of the arrays
     */
    public int intersectionOfArrays(int[][] arrs) {
        Comparator<Pair> comparator = new Comparator<Pair>() {
          public int compare(Pair x, Pair y) {
            return arrs[x.row][x.col] - arrs[y.row][y.col];
          }
        };
        
        Queue<Pair> queue = new PriorityQueue<>(arrs.length, comparator);
        
        for (int i = 0; i < arrs.length; i++) {
            if (arrs[i].length == 0) {
                return 0;
            }
            
            Arrays.sort(arrs[i]);
            queue.offer(new Pair(i, 0));
        }
        
        int lastValue = 0, count = 0;
        int intersection = 0;
        while (!queue.isEmpty()) {
            Pair pair = queue.poll();
            if (arrs[pair.row][pair.col] != lastValue || count == 0) {
                if (count == arrs.length) {
                  intersection++;
                }
                lastValue = arrs[pair.row][pair.col];
                count = 1;
            } else {
                count++;
            }
            
            pair.col++;
            if (pair.col < arrs[pair.row].length) {
              queue.offer(pair);
            }
        }
        
        // kickoff the last number
        if (count == arrs.length) {
            intersection++;
        }
        
        return intersection;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)