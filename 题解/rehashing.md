# 重哈希
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/rehashing/?utm_source=sc-github-wzz)
 ## 题目描述
 哈希表容量的大小在一开始是不确定的。如果哈希表存储的元素太多（如超过容量的十分之一），我们应该将哈希表容量扩大一倍，并将所有的哈希值重新安排。假设你有如下一哈希表：

`size=3`, `capacity=4`

	[null, 21, 14, null]
	       ↓    ↓
	       9   null
	       ↓
	      null


哈希函数为：

	int hashcode(int key, int capacity) {
	    return key % capacity;
	}

这里有三个数字9，14，21，其中21和9共享同一个位置因为它们有相同的哈希值1(21 % 4 = 9 % 4 = 1)。我们将它们存储在同一个链表中。

重建哈希表，将容量扩大一倍，我们将会得到：

`size=3`, `capacity=8`

	index:   0    1    2    3     4    5    6   7
	hash : [null, 9, null, null, null, 21, 14, null]

给定一个哈希表，返回重哈希后的哈希表。
 ### 样例说明
 ***样例 1***
```
输入 : [null, 21->9->null, 14->null, null]
输出 : [null, 9->null, null, null, null, 21->null, 14->null, null]
```

 ### 参考代码
 ```python
class Solution:
    def addlistnode(self, node, number):
        if node.next != None:
            self.addlistnode(node.next, number)
        else:
            node.next = ListNode(number)

    def addnode(self, anshashTable, number):
        p = number % len(anshashTable)
        if anshashTable[p] == None:
            anshashTable[p] = ListNode(number)
        else:
            self.addlistnode(anshashTable[p], number)

    def rehashing(self,hashTable):
        HASH_SIZE = 2 * len(hashTable)
        anshashTable = [None for i in range(HASH_SIZE)]
        for item in hashTable:
            p = item
            while p != None:
                self.addnode(anshashTable,p.val)
                p = p.next
        return anshashTable
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)