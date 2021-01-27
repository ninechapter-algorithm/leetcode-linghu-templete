# 动态数组 ArrayList
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/arraylist/?utm_source=sc-github-wzz)
 ## 题目描述
 用 ArrayList 实现一些操作：

1. `create(n)`. 创建一个大小为n的ArrayList，包含n个整数，依次为[0, 1, 2, ... n-1]
2. `clone(list)`. 克隆一个list。使得克隆后的list与原来的list是完全独立无关的。
3. `get(list, index)`. 查询list中index这个位置的数。
4. `set(list, index, val)`. 将list中index这个位置的数改为val。
5. `remove(list, index)`. 移除list中index这个位置的数。
6. `indexOf(list, val)`. 在list中查找值为val的数，返回它的index。如果没有返回-1。

请使用 ArrayList 的原生方法完成这些操作。参见Java文档：[ArrayList参考文档](https://docs.oracle.com/javase/7/docs/api/java/util/ArrayList.html "ArrayList 文档")
 ### 样例说明
 输入:

```plain
create(5)
get([0,1,2,3,4], 0)
get([0,1,2,3,4], 1)
get([0,1,2,3,4], 4)
clone([0,1,2,3,4])
get([0,1,2,3,4], 2)
indexOf([0,1,2,3,4], 1)
indexOf([0,1,2,3,4], 10)
remove([0,1,2,3,4], 3)
get([0,1,2,4], 3)
set([0,1,2,4], 2, 3)
get([0,1,2,3,4], 2)
get([0,1,2,3,4], 3)
```

输出:

```plain
[0,1,2,3,4]
0
1
4
[0,1,2,3,4]
2
1
-1
[0,1,2,4]
4
[0,1,3,4]
2
3
```

Explanation:

The code for java is like this:

```java
ArrayList<Integer> list = ArrayListManager.create(5);
list.get(0);  // 应该返回 0
list.get(1);  // 应该返回 1
list.get(4);  // 应该返回 4

// 被克隆的列表应该是 [0,1,2,3,4]
ArrayList<Integer> clone_list = ArrayListManager.clone(list);

ArrayListManager.get(list, 2);  // 应该返回 2
ArrayListManager.indexOf(list, 1); // 应该返回 1
ArrayListManager.indexOf(list, 10); // 应该返回 -1
ArrayListManager.remove(list, 3); // 列表将变成 [0, 1, 2, 4]
ArrayListManager.get(list, 3); // 因为3已经被移除，所以应该返回4
ArrayListManager.set(list, 2, 3); // 列表将变成 [0, 1, 3, 4]

clone_list.get(2); // 应该返回 2
clone_list.get(3); // 应该返回 3
```


 ### 参考代码
 ```java
public class ArrayListManager {
    /**
     * @param n: You should generate an array list of n elements.
     * @return: The array list your just created.
     */
    public static ArrayList<Integer> create(int n) {
        // Write your code here
        ArrayList<Integer> list = new ArrayList<Integer>();
        for (int i = 0; i < n; i++) {
            list.add(i);
        }
        return list;
    }
    
    /**
     * @param list: The list you need to clone
     * @return: A deep copyed array list from the given list
     */
    public static ArrayList<Integer> clone(ArrayList<Integer> list) {
        // Write your code here
        ArrayList<Integer> dist = new ArrayList<Integer>();
        for (Integer a : list)
            dist.add(a);
        return dist;
        //return list;
    }
    
    /**
     * @param list: The array list to find the kth element
     * @param k: Find the kth element
     * @return: The kth element
     */
    public static int get(ArrayList<Integer> list, int k) {
        // Write your code here
        return list.get(k);
    }
    
    /**
     * @param list: The array list
     * @param k: Find the kth element, set it to val
     * @param val: Find the kth element, set it to val
     */
    public static void set(ArrayList<Integer> list, int k, int val) {
        // write your code here
        list.set(k, val);
    }
    
    /**
     * @param list: The array list to remove the kth element
     * @param k: Remove the kth element
     */
    public static void remove(ArrayList<Integer> list, int k) {
        // write tour code here
        list.remove(k);
    }
    
    /**
     * @param list: The array list.
     * @param val: Get the index of the first element that equals to val
     * @return: Return the index of that element
     */
    public static int indexOf(ArrayList<Integer> list, int val) {
        // Write your code here
        if (list == null)
            return -1;
        return list.indexOf(val);
    }
}

```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)