# 反向索引
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/inverted-index/?utm_source=sc-github-wzz)
 ## 题目描述
 创建给定文档的反向索引
 ### 样例说明
 给出一个包括id与内容的文档list(我们提供了document类).
返回一个反向索引(hashmap的key是单词, value是文档的id).

例 1:
```
输入:
[
  {
    "id": 1,
    "content": "This is the content of document 1 it is very short"
  },
  {
    "id": 2,
    "content": "This is the content of document 2 it is very long bilabial bilabial heheh hahaha ..."
  },
]
输出:
{
   "This": [1, 2],
   "is": [1, 2],
   ...
}
```

例 2:
```
输入:
[
  {
    "id": 1,
    "content": "you are young"
  },
  {
    "id": 2,
    "content": "you are handsome"
  },
]
输出:
{
   "are": [1, 2],
   ...
}
```
 ### 参考代码
 利用hashmap创立反向索引
```python
'''
Definition of Document
class Document:
    def __init__(self, id, cotent):
        self.id = id
        self.content = content
'''
class Solution:
    # @param {Document[]} docs a list of documents
    # @return {dict(string, int[])} an inverted index
    def invertedIndex(self, docs):
        # Write your code here
        rt = {}
        for doc in docs:
            for word in doc.content.split():
                if word in rt:
                    if rt[word][-1] != doc.id:
                        rt[word].append(doc.id)
                else:
                    rt[word] = [doc.id]
        return rt
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)