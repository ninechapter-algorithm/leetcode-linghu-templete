# 主元素 III
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/majority-number-iii/?utm_source=sc-github-wzz)
 ## 题目描述
 <p>给定一个整型数组，找到主元素，它在数组中的出现次数严格大于数组元素个数的<font color="#e76363"><b>1/k</b></font>。<br></p>
 ### 样例说明
 例1:
```
输入: [3,1,2,3,2,3,3,4,4,4] and k=3, 
输出: 3.
```

例2:
```
输入: [1,1,2] and k=3, 
输出: 1.
```


 ### 参考代码
 在原方法的基础上，利用hashmap即可
```java
public class Solution {
    /**
     * @param nums: A list of integers
     * @param k: As described
     * @return: The majority number
     */
    public int majorityNumber(ArrayList<Integer> nums, int k) {
        // count at most k keys.
        HashMap<Integer, Integer> counters = new HashMap<Integer, Integer>();
        for (Integer i : nums) {
            if (!counters.containsKey(i)) {
                counters.put(i, 1);
            } else {
                counters.put(i, counters.get(i) + 1);
            }
            
            if (counters.size() >= k) {
                removeKey(counters);
            }
        }
        
        // corner case
        if (counters.size() == 0) {
            return Integer.MIN_VALUE;
        }
        
        // recalculate counters
        for (Integer i : counters.keySet()) {
            counters.put(i, 0);
        }
        for (Integer i : nums) {
            if (counters.containsKey(i)) {
                counters.put(i, counters.get(i) + 1);
            }
        }
        
        // find the max key
        int maxCounter = 0, maxKey = 0;
        for (Integer i : counters.keySet()) {
            if (counters.get(i) > maxCounter) {
                maxCounter = counters.get(i);
                maxKey = i;
            }
        }
        
        return maxKey;
    }
    
    private void removeKey(HashMap<Integer, Integer> counters) {
        Set<Integer> keySet = counters.keySet();
        List<Integer> removeList = new ArrayList<>();
        for (Integer key : keySet) {
            counters.put(key, counters.get(key) - 1);
            if (counters.get(key) == 0) {
                removeList.add(key);
            }
        }
        for (Integer key : removeList) {
            counters.remove(key);
        }
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)