# 一致性哈希 II
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/consistent-hashing-ii/?utm_source=sc-github-wzz)
 ## 题目描述
 在 Consistent Hashing I 中我们介绍了一个比较简单的一致性哈希算法，这个简单的版本有两个缺陷：

1. 增加一台机器之后，数据全部从其中一台机器过来，这一台机器的读负载过大，对正常的服务会造成影响。
2. 当增加到3台机器的时候，每台服务器的负载量不均衡，为1:1:2。

为了解决这个问题，引入了 micro-shards 的概念，一个更好的算法是这样：

1. 将 360° 的区间分得更细。从 0~359 变为一个 0 ~ n-1 的区间，将这个区间首尾相接，连成一个圆。
2. 当加入一台新的机器的时候，随机选择在圆周中撒 k 个点，代表这台机器的 k 个 micro-shards。
3. 每个数据在圆周上也对应一个点，这个点通过一个 hash function 来计算。
4. 一个数据该属于哪台机器负责管理，是按照该数据对应的圆周上的点在圆上顺时针碰到的第一个 micro-shard 点所属的机器来决定。

n 和 k在真实的 NoSQL 数据库中一般是 2^64 和 1000。

请实现这种引入了 micro-shard 的 consistent hashing 的方法。主要实现如下的三个函数：

1. `create(int n, int k)`
2. `addMachine(int machine_id)` // add a new machine, return a list of shard ids.
3. `getMachineIdByHashCode(int hashcode)` // return machine id
 ### 样例说明
 **样例 1:**

```
输入:
  create(100, 3)
  addMachine(1)
  getMachineIdByHashCode(4)
  addMachine(2)
  getMachineIdByHashCode(61)
  getMachineIdByHashCode(91)
输出: 
  [77,83,86]
  1
  [15,35,93]
  1
  2
```

**样例 2:**

```
输入: 
  create(10, 5)
  addMachine(1)
  getMachineIdByHashCode(4)
  addMachine(2)
  getMachineIdByHashCode(0)
  getMachineIdByHashCode(1)
  getMachineIdByHashCode(2)
  getMachineIdByHashCode(3)
  getMachineIdByHashCode(4)
  getMachineIdByHashCode(5)
输出: 
  [2,3,5,6,7]
  1
  [0,1,4,8,9]
  2
  2
  1
  1
  2
  1
```
 ### 参考代码
 ```java
public class Solution {

    public int n, k;
    public Set<Integer> ids = null;
    public Map<Integer, List<Integer>> machines = null;

    // @param n a positive integer
    // @param k a positive integer
    // @return a Solution object
    public static Solution create(int n, int k) {
        // Write your code here
        Solution solution = new Solution();
        solution.n = n;
        solution.k = k;
        solution.ids = new TreeSet<Integer>();
        solution.machines = new HashMap<Integer, List<Integer>>();
        return solution;
    }

    // @param machine_id an integer
    // @return a list of shard ids
    public List<Integer> addMachine(int machine_id) {
        // Write your code here
        Random ra = new Random();
        List<Integer> random_nums = new ArrayList<Integer>();
        for (int i = 0; i < k; ++i) {
            int index = ra.nextInt(n);
            while (ids.contains(index))
                index = ra.nextInt(n);
            ids.add(index);
            random_nums.add(index);
        }

        Collections.sort(random_nums);
        machines.put(machine_id, random_nums);
        return random_nums;
    }

    // @param hashcode an integer
    // @return a machine id
    public int getMachineIdByHashCode(int hashcode) {
        // Write your code here
        int distance = n + 1;
        int machine_id = 0;
        for (Map.Entry<Integer, List<Integer>> entry : machines.entrySet()) {
            int key = entry.getKey();
            List<Integer> random_nums = entry.getValue();
            for (Integer num : random_nums) {
                int d = num - hashcode;
                if (d < 0)
                    d += n;
                if (d < distance) {
                    distance = d;
                    machine_id = key;
                }
            }
        }
        return machine_id;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)