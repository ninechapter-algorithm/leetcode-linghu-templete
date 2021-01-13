# 网页爬虫
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/webpage-crawler/?utm_source=sc-github-wzz)
 ## 题目描述
 实现一个网页爬虫，去模拟爬取`http://www.wikipedia.org/`页面，让我们简化这个问题，使用存储url替代存储网页的内容。

你的爬虫应该做：
1. 调用 `HtmlHelper.parseUrls(url)` 从当前给出的这个url对用的网页内容中获取所有的urls
2. 只爬取wikipedia的界面，这个界面内容由LintCode模拟
3. 相同的页面不重复爬取
4. 初始的url为：`http://www.wikipedia.org/`
 ### 样例说明
 
 ### 参考代码
 ```python
"""
class HtmlHelper:
    # @param (string)
    # @return (list)
    @classmethod
    def parseUrls(url):
        # Get all urls from a webpage of given url. 
"""

import threading

class Solution:
    """
    @param url(string): a url of root page
    @return (list): all urls
    """
    def crawler(self, url):
        self.queue = [url]
        self.urlSet = set([url])
        self.threads = []
        
        self.bfs()
        
        for thread in self.threads:
            thread.join()
        
        return list(self.urlSet)
    
    def bfs(self):
        while len(self.queue):
            url = self.queue.pop(0)
            sub_urls = HtmlHelper.parseUrls(url)
            for sub_url in sub_urls:
                if not "wikipedia" in sub_url:
                    continue
                if sub_url in self.urlSet:
                    continue
                self.urlSet.add(sub_url)
                self.queue.append(sub_url)
                if threading.activeCount() < 3:
                    thread = threading.Thread(target = self.bfs, args = (self, ))
                    self.threads.append(thread)
                    thread.start()

"""
class HtmlHelper:
    # @param (string)
    # @return (list)
    @classmethod
    def parseUrls(url):
        # Get all urls from a webpage of given url. 
"""

import threading

class Solution:
    """
    @param url(string): a url of root page
    @return (list): all urls
    """
    def crawler(self, url):
        self.urlSet = set([url])        
        self.threads = []
        
        self.dfs(url)
        
        for thread in self.threads:
            thread.join()
        
        return list(self.urlSet)
        
        
    def dfs(self, url):
        subUrls = HtmlHelper.parseUrls(url)
        for subUrl in subUrls:
            if not "wikipedia" in subUrl:
                continue
            if subUrl in self.urlSet:
                continue
            
            self.urlSet.add(subUrl)
            if threading.activeCount() < 3:
                newThread = threading.Thread(target = self.dfs,
                    args = (subUrl, )) # 需要加个逗号....
                self.threads.append(newThread)
                newThread.start()
            else:
                self.dfs(subUrl)
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)