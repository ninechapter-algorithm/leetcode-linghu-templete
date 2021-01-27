# 前K个高频元素
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/top-k-frequent-elements/?utm_source=sc-github-wzz)
 ## 题目描述
 给定一个非空的整数数组，返回其中出现频率前 $k$ 高的元素。
 ### 样例说明
 **样例 1:**

```
输入: nums = [1,1,1,2,2,3], k = 2
输出: [1,2]
```

**样例 2:**

```
输入: nums = [1], k = 1
输出: [1]
```


 ### 参考代码
 这题可以通过最小堆或者桶排实现：
- 最小堆
因为最终需要返回前 k 个频率最大的元素，通过维护一个元素数目为 k 的最小堆，每次都将新的元素与堆顶端的元素（堆中频率最小的元素）进行比较，如果新的元素的频率比堆顶端的元素大，则弹出堆顶端的元素，将新的元素添加进堆中。最终，堆中的 k 个元素即为前 k 个高频元素。
- 桶排
将数组中的元素按照出现频次进行分组，即出现频次为 i 的元素存放在第 i 个桶。最后，从桶中逆序取出前 k 个元素。
```java
public class Solution {
    public List<Integer> topKFrequent(int[] nums, int k) {
        Map<Integer, Integer> hashmap = new HashMap<Integer, Integer>();
        PriorityQueue<Map.Entry<Integer, Integer>> queue = new PriorityQueue<Map.Entry<Integer, Integer>>(
            new Comparator<Map.Entry<Integer, Integer>>() {
                public int compare(Map.Entry<Integer, Integer> e1, Map.Entry<Integer, Integer> e2) {
                    return e1.getValue() - e2.getValue();
                }
            });
        for (int i = 0; i < nums.length; i++) {
            if (!hashmap.containsKey(nums[i])) {
                hashmap.put(nums[i], 1);
            } else {
                hashmap.put(nums[i], hashmap.get(nums[i]) + 1);
            }
        }
        
        for (Map.Entry<Integer, Integer> entry : hashmap.entrySet()) {
            if (queue.size() < k) {
                queue.offer(entry);
            } else if (queue.peek().getValue() < entry.getValue()) {
                queue.poll();
                queue.offer(entry);
            }
        }
        
        List<Integer> ans = new ArrayList<Integer>();
        for (Map.Entry<Integer, Integer> entry : queue)
            ans.add(entry.getKey());
        return ans;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)