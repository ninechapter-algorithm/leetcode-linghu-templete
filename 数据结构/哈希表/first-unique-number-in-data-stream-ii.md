# 数据流中第一个独特的数 II
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/first-unique-number-in-data-stream-ii/?utm_source=sc-github-wzz)
 ## 题目描述
 我们需要实现一个叫 `DataStream` 的数据结构。并且这里有 `两` 个方法需要实现：

1. `void add(number)` // 加一个新的数
2. `int firstUnique()` // 返回第一个独特的数
 ### 样例说明
 例1:
```
输入:
add(1)
add(2)
firstUnique()
add(1)
firstUnique()
输出:
[1,2]
```

例2:
```
输入:
add(1)
add(2)
add(3)
add(4)
add(5)
firstUnique()
add(1)
firstUnique()
add(2)
firstUnique()
add(3)
firstUnique()
add(4)
firstUnique()
add(5)
add(6)
firstUnique()
输出:
[1,2,3,4,5,6]
```


 ### 参考代码
 使用类似 LRU Cache 的做法来做。
hash 的 key 为 num，value 为对应的 linkedlist 上的 previous node
```python
class DataStream:

    def __init__(self):
        self.dummy = ListNode(0)
        self.tail = self.dummy
        self.num_to_prev = {}
        self.duplicates = set()
          
    """
    @param num: next number in stream
    @return: nothing
    """
    def add(self, num):
        if num in self.duplicates:
            return
        
        if num not in self.num_to_prev:
            self.push_back(num)            
            return
        
        # find duplicate, remove it from hash & linked list
        self.duplicates.add(num)
        self.remove(num)
    
    def remove(self, num):
        prev = self.num_to_prev.get(num)
        del self.num_to_prev[num]
        prev.next = prev.next.next
        if prev.next:
            self.num_to_prev[prev.next.val] = prev
        else:
            # if we removed the tail node, prev will be the new tail
            self.tail = prev

    def push_back(self, num):
        # new num add to the tail
        self.tail.next = ListNode(num)
        self.num_to_prev[num] = self.tail
        self.tail = self.tail.next

    """
    @return: the first unique number in stream
    """
    def firstUnique(self):
        if not self.dummy.next:
            return None
        return self.dummy.next.val
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)