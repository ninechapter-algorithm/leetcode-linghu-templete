# Insert Delete GetRandom O(1) - 允许重复
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/insert-delete-getrandom-o1-duplicates-allowed/?utm_source=sc-github-wzz)
 ## 题目描述
 设计一个数据结构，需要支持以下操作，且平均时间复杂度为 **O(1)**。
 ### 样例说明
 **样例 1:**
```
输入:
insert(1)
insert(1)
insert(2)
getRandom()
remove(1)

// 初始化一个空的容器
RandomizedCollection collection = new RandomizedCollection();

// 把 1 插入到这容器中。如果这个容器不含 1 则返回 true 
collection.insert(1);

// 把 1 插入到这容器中。如果这个容器含 1 则返回 false, 此时容器中含有 [1,1]。
collection.insert(1);

// 把 1 插入到这容器中， 返回 true, 此时容器中含有 [1,1,2].
collection.insert(2);

// getRandom 应该有 2/3 的概率返回 1 ，1/3 的概率返回 2。
collection.getRandom();

// 从容器中删去一个 1 ， 此时容器中含有 [1,2].
collection.remove(1);

// getRandom 应该可以同等概率的返回 1 和 2。
collection.getRandom();
```

**样例 2:**
```
输入:
insert(1)
insert(1)
getRandom()
remove(1)
```

 ### 参考代码
 用 LinkedHashSet 的版本
```java
public class RandomizedCollection {

    ArrayList<Integer> result;
    HashMap<Integer, LinkedHashSet<Integer>> map;
    
    public RandomizedCollection() {
        result = new ArrayList<Integer>();
        map = new HashMap<Integer, LinkedHashSet<Integer>>();
    }

    public boolean insert(int val) {
        boolean alreadyExists = map.containsKey(val);
        if(!alreadyExists) {
            map.put(val, new LinkedHashSet<Integer>());
        }
        map.get(val).add(result.size());
        result.add(val);
        return !alreadyExists;
    }
    
    public boolean remove(int val) {
        if(!map.containsKey(val)) {
            return false;
        }
        LinkedHashSet<Integer> valSet = map.get(val);
        int indexToReplace = valSet.iterator().next();
        
        int numAtLastPlace = result.get(result.size() - 1);
        LinkedHashSet<Integer> replaceWith = map.get(numAtLastPlace);
        
        result.set(indexToReplace, numAtLastPlace);
        
        valSet.remove(indexToReplace);
        
        if(indexToReplace != result.size() - 1) {
            replaceWith.remove(result.size() - 1);
            replaceWith.add(indexToReplace);
        }
        result.remove(result.size() - 1);
        
        if(valSet.isEmpty()) {
            map.remove(val);
        }
        return true;
    }
    public int getRandom() {
        return result.get((int)(Math.random() * result.size()));
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)