# N数组第K大元素
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/kth-largest-in-n-arrays/?utm_source=sc-github-wzz)
 ## 题目描述
 在N个数组中找到第K大元素
 ### 样例说明
 例1:
```
输入:
k = 3, [[9,3,2,4,7],[1,2,3,4,8]]
输出:
7
解释:
第三大的元素为 7。

```
例2:
```
输入:
k = 2, [[9,3,2,4,8],[1,2,3,4,2]]
输出:
8
解释:
最大的元素为 9，第二大的元素为 8，第三大的元素为 4 等等。

```

 ### 参考代码
 对每个数组排序，然后将每个数组的最小元素加入到优先队列中，每次从优先队列中pop出一个元素，然后push进同组的下一个元素，直到第k个
```java
import java.util.Comparator;  
import java.util.PriorityQueue;  
import java.util.Queue; 

class Node {
    public int value, from_id, index;
    public Node(int _v, int _id, int _i) {
        this.value = _v;
        this.from_id = _id;
        this.index = _i;
    }
}

public class Solution {
    /**
     * @param arrays a list of array
     * @param k an integer
     * @return an integer, K-th largest element in N arrays
     */
    public int KthInArrays(int[][] arrays, int k) {
        // Write your code here
        Queue<Node> queue =  new PriorityQueue<Node>(k, new Comparator<Node>() {  
                public int compare(Node o1, Node o2) {  
                    if (o1.value > o2.value)
                        return -1;
                    else if (o1.value < o2.value)
                        return 1;
                    else
                        return 0;
                }
            }); 

        int n = arrays.length;
        int i;
        for (i = 0; i < n; ++i) {
            Arrays.sort(arrays[i]);
            
            if (arrays[i].length > 0) {
                int from_id = i;
                int index = arrays[i].length - 1;
                int value = arrays[i][index];
                queue.add(new Node(value, from_id, index));
            }
        }

        for (i  = 0; i < k; ++i) {
            Node temp = queue.poll();
            int from_id = temp.from_id;
            int index = temp.index;
            int value = temp.value;
            
            if (i == k - 1)
                return value;
            
            if (index > 0) {
                index --;
                value = arrays[from_id][index];
                queue.add(new Node(value, from_id, index));
            }
        }

        return -1;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)