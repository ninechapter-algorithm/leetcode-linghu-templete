## 题目描述

给定一个字符串列表**words**，找到**words**最长的word，使得这个word可用**words**中的其他word一次一个字符地构建。如果有多个可选答案，则返回最长的且具有最小字典序的word。

**样例**

Ⅰ. 
Input: words = ["w","wo","wor","worl", "world"]

Output:"world"

Explanation: “world”可通过”w”, “wo”, “wor”, “worl”一次一个字符进行构建。

Ⅱ. 
Input: words = ["a", "banana", "app", "appl", "ap", "apply", "apple"]

Output:"apple"

Explanation: “apply”和”apple”都可以由其他字符构建。但”apple”的字典序要小于”apply”。

**注意：**

- 所有的输入字符只包含小写字符。

- words的长度在[1, 1000]范围内。

- words[i]的长度在[1, 30]范围内。

## 解题思路分析

### 方法一：直接采用暴力搜索。

对于每一个word，检查是否其前缀都在**words**中。可以用**words**构建set。初始化**ans**=””，**words**，对每个元素，在set中寻找是否有其所有前缀。如果当前word合题，且长度大于**ans，**或长度等于**ans**但字典序小于ans，则修改**ans**为当前word。也可以先对**words**排序，按照长度从小到大，长度相同按照字典顺序。这样只要word合题就修改ans。

**时间复杂度：**O(sum(w_i^2)),w_i表示words[i]的长度。对于每一个word，通过**哈希表**检查是否所有的前缀都在set当中需要O(w_i^2)。

**空间复杂度：**O(sum(w_i))用于创建set。

### 方法二：因为涉及到了字符串的前缀，所以使用Trie结构（一种字符串前缀树）。

先介绍Trie，如果已经了解Trie树可跳过这部分：

Trie，又称单词查找树或键树，是一种树形结构。典型应用是用于统计和排序大量的字符串（但不仅限于字符串），所以经常被搜索引擎系统用于文本词频统计。它的优点是：最大限度地减少无谓的字符串比较，查询效率比哈希表高。

它有3个基本性质：

1.根节点不包含字符，除根节点外每一个节点都只包含一个字符。

2.从根节点到某一节点，路径上经过的字符连接起来，为该节点对应的字符串。

3.每个节点的所有子节点包含的字符都不相同。

Trie中每个节点有一个特殊标记作为结束符号，通过该标记可以判断当前节点是否是一个字符串的终结节点。

下图是一个Trie树的例子，记录了to,tea,ted,ten,a,i,in,inn这些words（以蓝色结尾）。

![image](https://upload-images.jianshu.io/upload_images/20499064-17d3ba0de7e27075?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

把每个word放入Trie中，对Trie进行DFS，只搜索终结节点。每个找到的节点中（除了根）从根到该节点路径代表该节点的word。之后同方法一：如果当前word合题，且长度大于**ans，**或长度等于**ans**但字典序小于ans，则修改**ans**为当前word。

**时间复杂度：**O(sum(w_i))，w_i是words[i]的长度。这是构建和便利Trie的复杂度。如果使用BFS而不是DFS，并且把每个节点的子节点进行排序，那么我们就不需要再去检查当前的word时候比**ans**要好，后访问的节点一定要好于先访问的节点，但复杂度不变。

**空间复杂度：**O(sum(w_i))用于构建Trie。

更多题解参考：[LintCode/LeetCode 参考答案查询](http://www.jiuzhang.com/solution/longest-word-in-dictionary/?utm_source=sc-github-lm)

## 参考程序

![](https://github.com/ninechapter-algorithm/ninechapter-algorithm/blob/master/pictures/%E5%AD%97%E5%85%B8%E9%87%8C%E9%9D%A2%E7%9A%84%E6%9C%80%E9%95%BF%E5%8D%95%E8%AF%8D%20-%20%E9%A2%98%E8%A7%A3.png)

## 面试官角度分析

本题是一道**中等难度**的题目，主要考察了Hash表和Trie这两种数据结构，可以区分几类面试者。对于想到Hash表来实现方法一的面试者可以给出hire；对于会用Trie树实现方法二的面试者给出strong hire。

## LintCode相关问题

[442. 实现 Trie（前缀树）](http://www.lintcode.com/problem/implement-trie/?utm_source=sc-github-lm)
