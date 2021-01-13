# 滑动窗口的最大值
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/sliding-window-maximum/?utm_source=sc-github-wzz)
 ## 题目描述
 给出一个可能包含重复的整数数组，和一个大小为 *k* 的滑动窗口, 从左到右在数组中滑动这个窗口，找到数组中每个窗口内的最大值。
 ### 样例说明
 **样例 1:**
```
输入:
[1,2,7,7,8]
3
输出:
[7,7,8]

解释：
最开始，窗口的状态如下：`[|1, 2 ,7| ,7 , 8]`, 最大值为 `7`;
然后窗口向右移动一位：`[1, |2, 7, 7|, 8]`, 最大值为 `7`;
最后窗口再向右移动一位：`[1, 2, |7, 7, 8|]`, 最大值为 `8`.
```

**样例 2:**
```
输入:
[1,2,3,1,2,3]
5
输出:
[3,3]

解释:
最开始，窗口的状态如下： `[|1,2,3,1,2 | ,3]` , 最大值为`3`;
然后窗口向右移动一位.`[1, |2,3,1,2,3]`, 最大值为 `3`;
```
 ### 参考代码
 单调的双端队列
```java
// 九章算法强化班版本 
// deque中存储位置
public class Solution {
    int[] a;
    /**
     * @param nums: A list of integers.
     * @return: The maximum number inside the window at each moving.
     */
    void inQueue(Deque<Integer> deque, int pos) {
        while (!deque.isEmpty() && a[deque.peekLast()] <= a[pos]) {
            deque.pollLast();
        }
        deque.offer(pos);
    }
    
    void outQueue(Deque<Integer> deque, int pos) {
        if (deque.peekFirst() == pos) {
            deque.pollFirst();
        }
    }
    
    public ArrayList<Integer> maxSlidingWindow(int[] nums, int k) {
        a = nums;
        // write your code here
        ArrayList<Integer> ans = new ArrayList<Integer>();
        Deque<Integer> deque = new ArrayDeque<Integer>();
        if (nums.length == 0) {
            return ans;
        }
        for (int i = 0; i < k - 1; i++) {
            inQueue(deque, i);
        }
        
        for(int i = k - 1; i < nums.length; i++) {
            inQueue(deque, i);
            ans.add(a[deque.peekFirst()]);
            outQueue(deque, i - k + 1);
        }
        return ans;

    }
}

// 方法二

public class Solution {
    
    /**
     * @param nums: A list of integers.
     * @return: The maximum number inside the window at each moving.
     */
    void inQueue(Deque<Integer> deque, int num) {
        while (!deque.isEmpty() && deque.peekLast() < num) {
            deque.pollLast();
        }
        deque.offer(num);
    }
    
    void outQueue(Deque<Integer> deque, int num) {
        if (deque.peekFirst() == num) {
            deque.pollFirst();
        }
    }
    
    public ArrayList<Integer> maxSlidingWindow(int[] nums, int k) {
        // write your code here
    	ArrayList<Integer> ans = new ArrayList<Integer>();
        Deque<Integer> deque = new ArrayDeque<Integer>();
        if (nums.length == 0) {
            return ans;
        }
        for (int i = 0; i < k - 1; i++) {
            inQueue(deque, nums[i]);
        }
        
        for(int i = k - 1; i < nums.length; i++) {
            inQueue(deque, nums[i]);
            ans.add(deque.peekFirst());
            outQueue(deque, nums[i - k + 1]);
        }
        return ans;

    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)