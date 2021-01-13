# Top k largest Number II
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/top-k-largest-number-ii/?utm_source=sc-github-wzz)
 ## 题目描述
 1773
 ### 样例说明
 1773
 ### 参考代码
 <p><br></p>
```java
public class Solution {
    private int maxSize;
    private Queue<Integer> minheap;
    public Solution(int k) {
        minheap = new PriorityQueue<>();
        maxSize = k;
    }

    public void add(int num) {
        if (minheap.size() < maxSize) {
            minheap.offer(num);
            return;
        }
        
        if (num > minheap.peek()) {
            minheap.poll();
            minheap.offer(num);
        }
    }

    public List<Integer> topk() {
        Iterator it = minheap.iterator();
        List<Integer> result = new ArrayList<Integer>();
        while (it.hasNext()) {
            result.add((Integer) it.next());
        }
        Collections.sort(result, Collections.reverseOrder());
        return result;
    }
};
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)