# 两数之和 III-数据结构设计
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/two-sum-iii-data-structure-design/?utm_source=sc-github-wzz)
 ## 题目描述
 设计b并实现一个 TwoSum 类。他需要支持以下操作:`add` 和 `find`。
`add` -把这个数添加到内部的数据结构。
`find` -是否存在任意一对数字之和等于这个值
 ### 样例说明
 **样例 1:**
```
add(1);add(3);add(5);
find(4)//返回true
find(7)//返回false
```
 ### 参考代码
 ```java
public class TwoSum {

    private List<Integer> list = null;
    private Map<Integer, Integer> map = null;
    public TwoSum() {
        list = new ArrayList<Integer>();
        map = new HashMap<Integer, Integer>();
    }

    // Add the number to an internal data structure.
    public void add(int number) {
        // Write your code here
        if (map.containsKey(number)) {
            map.put(number, map.get(number) + 1);
        } else {
            map.put(number, 1);
            list.add(number);
        }
    }

    // Find if there exists any pair of numbers which sum is equal to the value.
    public boolean find(int value) {
        // Write your code here
        for (int i = 0; i < list.size(); i++) {
            int num1 = list.get(i), num2 = value - num1;
            if ((num1 == num2 && map.get(num1) > 1) || 
                (num1 != num2 && map.containsKey(num2))) 
                return true;
        }
        return false;
    }
}


// Your TwoSum object will be instantiated and called as such:
// TwoSum twoSum = new TwoSum();
// twoSum.add(number);
// twoSum.find(value);
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)