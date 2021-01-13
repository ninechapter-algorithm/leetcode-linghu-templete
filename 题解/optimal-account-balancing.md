# 最优账户结余
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/optimal-account-balancing/?utm_source=sc-github-wzz)
 ## 题目描述
 给一有向图,每一条边用一个 `三元组` 表示, 比如 `[u, v, w]` 代表权值为 `w` 的从 `u` 到 `v` 的一条边. 计算出保证每个点的权重相等需要添加的最少的边数. 也就是说, 指向这一点的边权重总和等于这个点指向其他点的边权重之和.
 ### 样例说明
 **样例1**

```plain
输入: [[0,1,10],[2,0,5]]
输出: 2
说明:
需要添加两条边
它们是 [1,0,5] 以及 [1,2,5]
```

**样例2**

```plain
输入: [[0,1,10],[1,0,1],[1,2,5],[2,0,5]]
输出: 1
说明:
只需要添加一条边 [1,0,4]
```


 ### 参考代码
 ```java
public class Solution {
    public int balanceGraph(int[][] transactions) {
        Map<Integer, Integer> debt = new HashMap<>();
        for(int[] t : transactions){       //预处理收支情况
            debt.put(t[0], debt.getOrDefault(t[0], 0) - t[2]);
            debt.put(t[1], debt.getOrDefault(t[1], 0) + t[2]);
        }
        int[] account = new int[debt.size()];
        int len = 0;
        for(int v : debt.values()){         //去除收支平衡的人
            if(v != 0){
                account[len++] = v;
            }
        }
        
        if(len == 0) 
          return 0;
        
        int[] dp = new int[1 << len];
        Arrays.fill(dp, Integer.MAX_VALUE/2);
        for(int i = 1; i <  dp.length; i++){   //枚举每个子集
        
            int sum = 0, count = 0;
            for(int j = 0; j < len; j++){
                if((1<<j & i) != 0){         //这个子集里有第j个人
                    sum += account[j];             //加上他的收支情况
                    count++;                 //平衡这个子集需要的最大交易数
                }
            }
           
            if(sum == 0){                    //如果这个子集的收支平衡，那么它是一个子问题
                dp[i] = count - 1;           //这个子集需要的最大交易数
                for(int j = 1; j < i; j++){  //枚举这个子问题的子集
                    if(((i & j) == j) && dp[j] + dp[i-j] < dp[i]){
                        dp[i] = dp[j] + dp[i - j];  //求这个子问题的最优解
                    } 
                }
            }
        }
        return dp[dp.length - 1];            //返回总问题的最优解
        
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)