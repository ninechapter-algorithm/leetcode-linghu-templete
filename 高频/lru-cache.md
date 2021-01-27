# LRU缓存策略
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/lru-cache/?utm_source=sc-github-wzz)
 ## 题目描述
 为最近最少使用（LRU）缓存策略设计一个数据结构，它应该支持以下操作：获取数据和写入数据。

- `get(key)` 获取数据：如果缓存中存在key，则获取其数据值（通常是正数），否则返回-1。
- `set(key, value)` 写入数据：如果key还没有在缓存中，则写入其数据值。当缓存达到上限，它应该在写入新数据之前删除最近最少使用的数据用来腾出空闲位置。

最终, 你需要返回每次 `get` 的数据.
 ### 样例说明
 **样例 1:**
```
输入：
LRUCache(2)
set(2, 1)
set(1, 1)
get(2)
set(4, 1)
get(1)
get(2)
输出：[1,-1,1]
解释：
cache上限为2，set(2,1)，set(1, 1)，get(2) 然后返回 1，set(4,1) 然后 delete (1,1)，因为 （1,1）最少使用，get(1) 然后返回 -1，get(2) 然后返回 1。
```

**样例 2:**
```
输入：
LRUCache(1)
set(2, 1)
get(2)
set(3, 2)
get(2)
get(3)
输出：[1,-1,2]
解释：
cache上限为 1，set(2,1)，get(2) 然后返回 1，set(3,2) 然后 delete (2,1)，get(2) 然后返回 -1，get(3) 然后返回 2。
```
 ### 参考代码
 Singly Linked List 的版本
```
[[java]]
public class LRUCache {
    class ListNode {
        public int key, val;
        public ListNode next;
        
        public ListNode(int key, int val) {
            this.key = key;
            this.val = val;
            this.next = null;
        }
    }
    
    private int capacity, size;
    private ListNode dummy, tail;
    private Map<Integer, ListNode> keyToPrev;

    /*
    * @param capacity: An integer
    */
    public LRUCache(int capacity) {
        this.capacity = capacity;
        this.keyToPrev = new HashMap<Integer, ListNode>();
        this.dummy = new ListNode(0, 0);
        this.tail = this.dummy;
    }

    private void moveToTail(int key) {
        ListNode prev = keyToPrev.get(key);
        ListNode curt = prev.next;
        
        if (tail == curt) {
            return;
        }
        
        prev.next = prev.next.next;
        tail.next = curt;
        curt.next = null;
        
        if (prev.next != null) {
            keyToPrev.put(prev.next.key, prev);
        }
        keyToPrev.put(curt.key, tail);
        
        tail = curt;
    }
    
    /*
     * @param key: An integer
     * @return: An integer
     */
    public int get(int key) {
        if (!keyToPrev.containsKey(key)) {
            return -1;
        }
        
        moveToTail(key);
        
        // the key has been moved to the end
        return tail.val;
    }
    
    /*
     * @param key: An integer
     * @param value: An integer
     * @return: nothing
     */
    public void set(int key, int value) {
        // get method will move the key to the end of the linked list
        if (get(key) != -1) {
            ListNode prev = keyToPrev.get(key);
            prev.next.val = value;
            return;
        }
        
        if (size < capacity) {
            size++;
            ListNode curt = new ListNode(key, value);
            tail.next = curt;
            keyToPrev.put(key, tail);
            
            tail = curt;
            return;
        }
        
        // replace the first node with new key, value
        ListNode first = dummy.next;
        keyToPrev.remove(first.key);
        
        first.key = key;
        first.val = value;
        keyToPrev.put(key, dummy);
        
        moveToTail(key);
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)