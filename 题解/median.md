# 中位数
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/median/?utm_source=sc-github-wzz)
 ## 题目描述
 <p>给定一个未排序的整数数组，找到其中位数。</p><p>中位数是排序后数组的中间值，如果数组的个数是偶数个，则返回排序后数组的第N/2个数。</p>
 ### 样例说明
 **样例 1:**
```
输入：[4, 5, 1, 2, 3]
输出：3
解释：
经过排序，得到数组[1,2,3,4,5]，中间数字为3
```
**样例 2:**
```
输入：[7, 9, 4, 5]
输出：5
解释：
经过排序，得到数组[4,5,7,9]，第二个(4/2)数字为5
```
 ### 参考代码
 考点：
* 区间第k大元素的查找

题解：
使用优先队列维护大小为k的有序集合，优先队列大小小于k时直接压入，等于k时与首个元素判断大小关系，小于时直接压入，并将首个元素弹出。最后输出优先队列的头部元素即可。
优先队列：
* 优先队列中，元素被赋予优先级。当访问元素时，具有最高优先级的元素最先删除。优先队列具有最高级先出的行为特征。通常采用堆数据结构来实现。
* 默认情况下，优先队列按照非递增顺序排列。
```cpp
class Solution {
public:
    /**
     * @param nums: A list of integers.
     * @return: An integer denotes the middle number of the array.
     */
    int median(vector<int> &nums) {
        // write your code here
        int k = (nums.size() + 1) / 2;
        priority_queue<int> que;
        int len = nums.size();
        for(int i = 0; i < len; i ++) {
            if(que.size() == k) {
                if(nums[i] < que.top()) {
                    que.pop();
                    que.push(nums[i]);
                }
            }else {
                que.push(nums[i]);
            }
        }
        return que.top();
    }
};
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)