# 两个排序数组和的第K小
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/kth-smallest-sum-in-two-sorted-arrays/?utm_source=sc-github-wzz)
 ## 题目描述
 给定两个排好序的数组 *A*, *B*，定义集合 *sum* = *a* + *b* ，其中a来自A数组，b来自B数组，求 *sum* 中第k小的元素
 ### 样例说明
 **样例1**

```plain
输入:
a = [1, 7, 11]
b = [2, 4, 6]
k = 3
输出: 7
说明: 满足条件的所有的和有[3, 5, 7, 9, 11, 13, 13, 15, 17]，其中第三个是7.
```

**样例2**

```plain
输入:
a = [1, 7, 11]
b = [2, 4, 6]
k = 4
输出: 9
说明: 满足条件的所有的和有[3, 5, 7, 9, 11, 13, 13, 15, 17]，其中第四个是9.
```

**样例3**

```plain
输入:
a = [1, 7, 11]
b = [2, 4, 6]
k = 8
输出: 15
说明: 满足条件的所有的和有[3, 5, 7, 9, 11, 13, 13, 15, 17]，其中第八个是15.
```


 ### 参考代码
 类似于 Kth smallest in sorted matrix 一题。
使用 heapq
我们把行和列分别定为两个数组，就可以形成一个排好序的矩阵
```java
// 方法一
class Pair {
    public int x, y, sum;
    public Pair(int x, int y, int val) {
        this.x = x;
        this.y = y;
        this.sum = val;
    }
}
class PairComparator implements Comparator<Pair> {
    public int compare(Pair a, Pair b) {
        return a.sum - b.sum;
    }
}

public class Solution {
    /**
     * @param A an integer arrays sorted in ascending order
     * @param B an integer arrays sorted in ascending order
     * @param k an integer
     * @return an integer
     */
    public int kthSmallestSum(int[] A, int[] B, int k) {
        int[] dx = new int[]{0, 1};
        int[] dy = new int[]{1, 0};
        boolean[][] hash = new boolean[A.length][B.length];
        PriorityQueue<Pair> minHeap = new PriorityQueue<Pair>(k, new PairComparator());
        minHeap.add(new Pair(0, 0, A[0] + B[0]));

        for(int i = 0; i < k - 1; i ++){
            Pair cur = minHeap.poll();
            for(int j = 0; j < 2; j ++){
                int next_x = cur.x + dx[j];
                int next_y = cur.y + dy[j];
                Pair next_Pair = new Pair(next_x, next_y, 0);
                if(next_x < A.length && next_y < B.length &&  !hash[next_x][next_y]){
                    hash[next_x][next_y] = true;
                    next_Pair.sum = A[next_x] + B[next_y];
                    minHeap.add(next_Pair);
                }
            }
        }
        return minHeap.peek().sum;
    }
}

//方法二:
class Pair implements Comparable<Pair> {
    int x;
    int y;
    int sum;
    Pair(int x, int y, int sum) {
        this.x = x;
        this.y = y;
        this.sum = sum;
    }
    @Override
    public int compareTo(Pair another) {
        if (this.sum == another.sum) {
            return 0;
        }
        return this.sum < another.sum ? -1 : 1;
    }
    @Override
    public boolean equals(Object obj) {
        if (obj == this) {
            return true;
        } else if (!(obj instanceof Pair)) {
            return false;
        }
        Pair another = (Pair) obj;
        return this.x == another.x && this.y == another.y;
    }
    @Override
    public int hashCode() {
        return x * 101 + y;
    }
}
public class Solution {
    /**
     * @param A an integer arrays sorted in ascending order
     * @param B an integer arrays sorted in ascending order
     * @param k an integer
     * @return an integer
     */
    int[] dx = {1, 0};
    int[] dy = {0, 1};
    public int kthSmallestSum(int[] A, int[] B, int k) {
        if (A.length == 0 && B.length == 0) {
            return 0; 
        } else if (A.length == 0) {
            return B[k];
        } else if (B.length == 0) {
            return A[k];
        }
        HashSet<Pair> isVisited = new HashSet<Pair>();
        PriorityQueue<Pair> minHeap = new PriorityQueue<Pair>();
        Pair p;
        Pair nextP;
        p = new Pair(0, 0, A[0] + B[0]);
        minHeap.offer(p);
        isVisited.add(p);
        int nextX;
        int nextY;
        int nextSum;
        for (int count = 0; count < k - 1; count++) {
            p = minHeap.poll();
            for (int i = 0; i < 2; i++) {
                nextX = p.x + dx[i];
                nextY = p.y + dy[i];
                nextP = new Pair(nextX, nextY, 0);
                if (nextX >= 0 && nextX < A.length && nextY >= 0 && nextY < B.length && !isVisited.contains(nextP)) {
                    nextSum = A[nextX] + B[nextY];
                    nextP.sum = nextSum;
                    minHeap.offer(nextP);
                    isVisited.add(nextP);
                }
            }
        }
        return minHeap.peek().sum;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)