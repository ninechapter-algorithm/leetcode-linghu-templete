# 分糖果
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/candy/?utm_source=sc-github-wzz)
 ## 题目描述
 有 `N` 个小孩站成一列。每个小孩有一个评级。给定数组 `ratings` 代表这些小孩的评级。

现在你需要按照以下要求，给小孩们分糖果：

* 每个小孩至少得到一颗糖果。 

* 评级越高的小孩可以比他相邻的两个小孩得到更多的糖果。

你最少要准备多少糖果？
 ### 样例说明
 
 ### 参考代码
 初始假定给每个小孩都分一颗糖果, 即设定一个全1的 count 数组.

然后我们开始修正这个数组:

首先从左到右遍历, 如果发现一个小孩左边的小孩比自己的 rating 低, 那么把这个小孩的糖果数设为他左边的小孩 + 1

这时我们分配的糖果已经满足了: 评分更高的小孩比他左边的小孩获得更多的糖果. 然后我们再从右往左遍历一次就可以了. 

但是这时还应该注意一点: 当一个小孩右边的小孩比自己的 rating 低时, 这个小孩的糖果可能已经比他右边的小孩多了, 而且可能多不止一个, 这时应该保留他的糖果数目不变.

比如这组数据: [1, 2, 3, 4, 1], 初始 count 数组为 [1, 1, 1, 1, 1], 第一次遍历之后变成 [1, 2, 3, 4, 1], 第二次遍历不应该再改变这个数组了.
```python
class Solution:
    # @param ratings, a list of integer
    # @return an integer
    def candy(self, ratings):
        candynum = [1 for i in range(len(ratings))]
        for i in range(1, len(ratings)):
            if ratings[i] > ratings[i-1]:
                candynum[i] = candynum[i-1] + 1
        for i in range(len(ratings)-2, -1, -1):
            if ratings[i+1] < ratings[i] and candynum[i+1] >= candynum[i]:
                candynum[i] = candynum[i+1] + 1
        return sum(candynum)
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)