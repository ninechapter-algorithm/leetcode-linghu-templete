# Insert Delete GetRandom O(1)

 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/insert-delete-getrandom-o1/?utm_source=sc-github-wzz)
 ## 题目描述
 设计一个数据结构实现在平均 `O(1)` 的复杂度下执行以下所有的操作。

* `insert(val)`: 如果这个元素不在set中，则插入。

* `remove(val)`: 如果这个元素在set中，则从set中移除。

* `getRandom`: 随机从set中返回一个元素。每一个元素返回的可能性必须相同。
 ### 样例说明
 ```
// 初始化空集set
RandomizedSet randomSet = new RandomizedSet();

// 1插入set中。返回正确因为1被成功插入
randomSet.insert(1);

// 返回错误因为2不在set中
randomSet.remove(2);

// 2插入set中，返回正确，set现在有[1,2]。
randomSet.insert(2);

// getRandom 应该随机的返回1或2。
randomSet.getRandom();

// 从set中移除1，返回正确。set现在有[2]。
randomSet.remove(1);

// 2已经在set中，返回错误。
randomSet.insert(2);

// 因为2是set中唯一的数字，所以getRandom总是返回2。
randomSet.getRandom();
```
 ### 参考代码
 使用数组来保存当前集合中的元素，同时用一个hashMap来保存数字与它在数组中下标的对应关系。

插入操作时：
* 若已存在此元素返回false
* 不存在时将新的元素插入数组最后一位，同时更新hashMap。

删除操作时：
* 若不存在此元素返回false
* 存在时先根据hashMap得到要删除数字的下标，再将数组的最后一个数放到需要删除的数的位置上，删除数组最后一位，同时更新hashMap。

获取随机数操作时：
* 根据数组的长度来获取一个随机的下标，再根据下标获取元素。
```java
import java.util.Random;
public class RandomizedSet {

    ArrayList<Integer> nums;
    HashMap<Integer, Integer> num2index;
    Random rand;

    public RandomizedSet() {
        // do initialize if necessary 
        nums = new ArrayList<Integer>();
        num2index = new HashMap<Integer, Integer>();  
        rand = new Random();
    }
    
    // Inserts a value to the set
    // Returns true if the set did not already contain the specified element or false
    public boolean insert(int val) {
        if (num2index.containsKey(val)) {
            return false;
        }
        
        num2index.put(val, nums.size());
        nums.add(val);
        return true;
    }
    
    // Removes a value from the set
    // Return true if the set contained the specified element or false
    public boolean remove(int val) {
        if (!num2index.containsKey(val)) {
            return false; 
        } 
        
        int index = num2index.get(val);
        if (index < nums.size() - 1) { // not the last one than swap the last one with this val
            int last = nums.get(nums.size() - 1);
            nums.set(index, last);
            num2index.put(last, index);
        }
        num2index.remove(val);
        nums.remove(nums.size() - 1);
        return true;
    }
    
    // Get a random element from the set
    public int getRandom() {
        return nums.get(rand.nextInt(nums.size()));
    }
}

/**
 * Your RandomizedSet object will be instantiated and called as such:
 * RandomizedSet obj = new RandomizedSet();
 * boolean param = obj.insert(val);
 * boolean param = obj.remove(val);
 * int param = obj.getRandom();
 */
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)