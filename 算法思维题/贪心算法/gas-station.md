# 加油站
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/gas-station/?utm_source=sc-github-wzz)
 ## 题目描述
 在一条环路上有 _N_ 个加油站，其中第 _i_ 个加油站有汽油`gas[i]`，并且从第_i_个加油站前往第_i_+1个加油站需要消耗汽油`cost[i]`。

你有一辆油箱容量无限大的汽车，现在要从某一个加油站出发绕环路一周，一开始油箱为空。

求可环绕环路一周时出发的加油站的编号，若不存在环绕一周的方案，则返回`-1`。
 ### 样例说明
 **样例 1:**
```
输入:gas[i]=[1,1,3,1],cost[i]=[2,2,1,1]
输出:2
```

**样例 2:**
```
输入:gas[i]=[1,1,3,1],cost[i]=[2,2,10,1]
输出:-1
```

 ### 参考代码
 There are N gas stations along a circular route, where the amount of gas at station i is gas[i].&nbsp;<div>You have a car with an unlimited gas tank and it costs cost[i] of gas to travel from station i to its next station (i+1). You begin the journey with an empty tank at one of the gas stations.&nbsp;</div><div>Return the starting gas station's index if you can travel around the circuit once, otherwise return -1.&nbsp;</div><div>Note:&nbsp;</div><div>The solution is guaranteed to be unique.<div><br></div><div><span style="color: rgb(102, 110, 112); font-family: 'Open Sans', Arial, sans-serif; line-height: 22.3999996185303px;">详细题解请见九章算法微博:</span><span style="color: rgb(102, 110, 112); font-family: 'Open Sans', Arial, sans-serif; line-height: 22.3999996185303px;">&nbsp;&nbsp;</span><a href="http://weibo.com/3948019741/BC431fkFU" target="_blank">http://weibo.com/3948019741/BC431fkFU</a><br></div></div>
```java
public class Solution {
    public int canCompleteCircuit(int[] gas, int[] cost) {
        if (gas == null || cost == null || gas.length == 0 || cost.length == 0) {
            return -1;
        }

        int sum = 0;
        int total = 0;
        int index = -1;

        for(int i = 0; i<gas.length; i++) {
            sum += gas[i] - cost[i];
            total += gas[i] - cost[i];
            if(sum < 0) {
                index = i;
                sum = 0;
            }
        }
        return total < 0 ? -1 : index + 1;
        // index should be updated here for cases ([5], [4]);
        // total < 0 is for case [2], [2]
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)