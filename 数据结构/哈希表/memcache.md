# 内存缓存
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/memcache/?utm_source=sc-github-wzz)
 ## 题目描述
 实现下列几个方法：
1.`get(curtTime, key)`. 得到key的值，如果不存在返回2147483647
2.`set(curtTime, key, value, ttl)`. 设置一个pair(key,value)，有效期从curtTime到curtTime + ttl -1 , 如果ttl为0，则一直存在
3.`delete(curtTime, key)`. 删除这个key
4.`incr(curtTime, key, delta)`. 给key的value加上delta，并且返回 如果不存在返回 2147483647。
5.`decr(curtTime, key, delta)`. 给key的value减去delta，并且返回 如果不存在返回 2147483647。
 ### 样例说明
 **样例1**

```
get(1, 0)
>> 2147483647
set(2, 1, 1, 2)
get(3, 1)
>> 1
get(4, 1)
>> 2147483647
incr(5, 1, 1)
>> 2147483647
set(6, 1, 3, 0)
incr(7, 1, 1)
>> 4
decr(8, 1, 1)
>> 3
get(9, 1)
>> 3
delete(10, 1)
get(11, 1)
>> 2147483647
incr(12, 1, 1)
>> 2147483647
```**样例1**

```
get(1, 0)
>> 2147483647
set(2, 1, 1, 2)
get(3, 1)
>> 1
get(4, 1)
>> 2147483647
incr(5, 1, 1)
>> 2147483647
set(6, 1, 3, 0)
incr(7, 1, 1)
>> 4
decr(8, 1, 1)
>> 3
get(9, 1)
>> 3
delete(10, 1)
get(11, 1)
>> 2147483647
incr(12, 1, 1)
>> 2147483647
```
 ### 参考代码
 ```java
class Resource {
    public int value;
    public int expired;
    public Resource(int value, int expired) {
        this.value = value;
        this.expired = expired;
    }
}

public class Memcache {

    Map<Integer, Resource> client = null;

    public Memcache() {
        // Initialize your data structure here.
        client = new HashMap<Integer, Resource>();
    }

    public int get(int curtTime, int key) {
        // Write your code here
        if (!client.containsKey(key))
            return Integer.MAX_VALUE;

        Resource res = client.get(key);
        if (res.expired >= curtTime || res.expired == -1)
            return res.value;
        else
            return Integer.MAX_VALUE;
    }

    public void set(int curtTime, int key, int value, int ttl) {
        // Write your code here
        int expired;
        if (ttl == 0)
            expired = -1;
        else
            expired = curtTime + ttl - 1;
        client.put(key, new Resource(value, expired));
    }

    public void delete(int curtTime, int key) {
        // Write your code here
        if (!client.containsKey(key))
            return;
        client.remove(key);
    }
    
    public int incr(int curtTime, int key, int delta) {
        // Write your code here
        if (get(curtTime, key) == Integer.MAX_VALUE)
            return Integer.MAX_VALUE;
        client.get(key).value += delta;
        return client.get(key).value;
    }

    public int decr(int curtTime, int key, int delta) {
        // Write your code here
        if (get(curtTime, key) == Integer.MAX_VALUE)
            return Integer.MAX_VALUE;
        client.get(key).value -= delta;
        return client.get(key).value;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)