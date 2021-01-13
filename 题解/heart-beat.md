# 心跳
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/heart-beat/?utm_source=sc-github-wzz)
 ## 题目描述
 在Master-Slave结构模式中，slave端会每隔k秒向master端发送ping请求表示自己还在运行。如果master端在 2 * k 秒内没有接收到任何来自slave的ping请求，那么master端会向管理员发送一个警告(比如发送一个电子邮件)。

现在让我们来模拟master端，你需要实现以下三个功能：
1.`initialize(slaves_ip_list, k)`，slaves_ip_list是所有slaves的ip地址列表，k为一个定值。
2.`ping(timestamp, slave_ip)`，这个方法在master端从slave端收到ping请求时执行，timestamp指当前的时间戳，slave_ip代表当前发送请求的slave端的ip地址
3.`getDiedSlaves(timestamp)`，这个方法会定期的(两次执行之间的时间间隔不确定)执行，timestamp代表当前的时间戳，此方法需要返回不再运行的slave端的所有ip地址列表，如果没有发现则返回空集合。

你可以假设当master端开始运行的时候时间戳为0，所有的方法都会根据全局的增长的时间戳来运行。
 ### 样例说明
 **样例1**

```
输入: 
initialize(["10.173.0.2", "10.173.0.3"], 10)
ping(1, "10.173.0.2")
getDiedSlaves(20)
getDiedSlaves(21)
ping(22, "10.173.0.2")
ping(23, "10.173.0.3")
getDiedSlaves(24)
getDiedSlaves(42)

输出: 
["10.173.0.3"]
["10.173.0.2", "10.173.0.3"]
[]
["10.173.0.2"]

解释:
initialize(["10.173.0.2", "10.173.0.3"], 10)
ping(1, "10.173.0.2")
getDiedSlaves(20)
>> ["10.173.0.3"]
getDiedSlaves(21)
>> ["10.173.0.2", "10.173.0.3"]
ping(22, "10.173.0.2")
ping(23, "10.173.0.3")
getDiedSlaves(24)
>> []
getDiedSlaves(42)
>> ["10.173.0.2"]
```

 ### 参考代码
 ```java
public class HeartBeat {

    public Map<String, Integer> slaves_ip_list;
    public int k;

    public HeartBeat() {
        // initialize your data structure here
        slaves_ip_list = new HashMap<String, Integer>();
    }

    // @param slaves_ip_list a list of slaves'ip addresses
    // @param k an integer
    // @return void
    public void initialize(List<String> slaves_ip_list, int k) {
        // Write your code here
        this.k = k;
        for (String ip : slaves_ip_list)
            this.slaves_ip_list.put(ip, 0);
    }

    // @param timestamp current timestamp in seconds
    // @param slave_ip the ip address of the slave server
    // @return nothing
    public void ping(int timestamp, String slave_ip) {
        // Write your code here
        if (!slaves_ip_list.containsKey(slave_ip))
            return;
        
        slaves_ip_list.put(slave_ip, timestamp);
    }

    // @param timestamp current timestamp in seconds
    // @return a list of slaves'ip addresses that died
    public List<String> getDiedSlaves(int timestamp) {
        // Write your code here
        List<String> results = new ArrayList<String>();
        
        Iterator iter = slaves_ip_list.entrySet().iterator();
        while (iter.hasNext()) {
            Map.Entry entry = (Map.Entry)iter.next();
            String ip = (String) entry.getKey();
            int time = (Integer) entry.getValue();
            if (time <= timestamp - 2 * k)
                results.add(ip);
        }
        return results;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)