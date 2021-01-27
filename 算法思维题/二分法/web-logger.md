# 网页日志
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/web-logger/?utm_source=sc-github-wzz)
 ## 题目描述
 实现下面两个方法：
1.`hit(timestamp)` 建立一个时间戳
2.`get_hit_count_in_last_5_minutes(timestamp)` 得到最后5分钟时间戳个数
 ### 样例说明
 **样例 1:**

```
输入:
  hit(1);
  hit(2);
  get_hit_count_in_last_5_minutes(3);
  hit(300);
  get_hit_count_in_last_5_minutes(300);
  get_hit_count_in_last_5_minutes(301);
输出: 
  2
  3
  2
```

**样例 2:**

```
输入: 
  hit(1)
  hit(1)
  hit(1)
  hit(2)
  get_hit_count_in_last_5_minutes(3)
  hit(300)
  get_hit_count_in_last_5_minutes(300)
  get_hit_count_in_last_5_minutes(301)
  get_hit_count_in_last_5_minutes(302)
  get_hit_count_in_last_5_minutes(900)
输出: 
  4
  5
  2
  1
  0
  0
```
 ### 参考代码
 因为 `timestamp` 是递增的, 所以我们可以用一个队列储存所有的记录.

- `hit(timestamp)` 直接将 `timestamp` 放到队尾
- `get_hit_count_in_last_5_minutes(timestamp)` 弹出队首, 直到队首元素与 `timestamp` 差距在300内为止, 返回队列大小即可

其中, 弹出元素的过程可以优化, 使用二分查找确定最大的小于 `timestamp - 300` 的元素.
```python
class WebLogger:
    
    def __init__(self):
        self.Q = []

    """
    @param: timestamp: An integer
    @return: nothing
    """
    def hit(self, timestamp):
        self.Q.append(timestamp)

    """
    @param: timestamp: An integer
    @return: An integer
    """
    def get_hit_count_in_last_5_minutes(self, timestamp):
        if self.Q == []:
            return 0
        i = 0
        n = len(self.Q)
        while i < n and self.Q[i] + 300 <= timestamp:
            i += 1
        self.Q = self.Q[i:]
        return len(self.Q)
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)