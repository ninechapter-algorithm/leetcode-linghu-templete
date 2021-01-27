# 二进制手表
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/binary-watch/?utm_source=sc-github-wzz)
 ## 题目描述
 给了一个二进制显示时间的手表和一个非负整数 `n`, `n` 代表在给定时间表上 `1` 的数量, 返回所有可能的时间
 ### 样例说明
 **样例1**
```
输入： 1
输出： ["1:00", "2:00", "4:00", "8:00", "0:01", "0:02", "0:04", "0:08", "0:16", "0:32"]
```
**样例2**
```
输入： 2
输出： ["0:03","0:05","0:06","0:09","0:10","0:12","0:17","0:18","0:20","0:24","0:33","0:34","0:36","0:40","0:48","10:00","1:01","1:02","1:04","1:08","1:16","1:32","2:01","2:02","2:04","2:08","2:16","2:32","3:00","4:01","4:02","4:04","4:08","4:16","4:32","5:00","6:00","8:01","8:02","8:04","8:08","8:16","8:32","9:00"]
```
 ### 参考代码
 遍历所有1的数量为num的二进制数，找出符合条件的数即可。
```java
public class Solution {
    public List<String> readBinaryWatch(int num) {
        ArrayList<String> ans = new ArrayList<String>();
        ArrayList<ArrayList<Integer>> hour = new ArrayList<ArrayList<Integer>>();
        ArrayList<ArrayList<Integer>> min = new ArrayList<ArrayList<Integer>>();
    for(int i = 0; i < 4; i++) {
        hour.add(new ArrayList<Integer>());
    }
    for(int i = 0; i < 6; i++) {
        min.add(new ArrayList<Integer>());
    }
        for(int i = 0; i < 12; i++) {
            int n = Integer.bitCount(i);
            hour.get(n).add(i);
        }
        for(int i = 0; i < 60; i++) {
            min.add(new ArrayList<Integer>());
            int n = Integer.bitCount(i);
            min.get(n).add(i);
        }
        for(int i = 0; i <= num && i < 4; i++) {
            for(int h = 0; h < hour.get(i).size(); h++) {
                for(int m = 0; m < min.get(num - i).size() && num - i < 6; m++) {
                    String string = hour.get(i).get(h).toString() + ":";
                    if(min.get(num - i).get(m) < 10) {
                        string += "0";
                    }
                    string += min.get(num - i).get(m).toString();
                    ans.add(string);
                }
            }
        }
        return ans;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)