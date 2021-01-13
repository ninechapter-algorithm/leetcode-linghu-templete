# Populating Next Right Pointers in Each Node
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/populating-next-right-pointers-in-each-node/?utm_source=sc-github-wzz)
 ## 题目描述
 1730
 ### 样例说明
 1730
 ### 参考代码
 Given a binary tree&nbsp;<div><br></div><div>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;struct TreeLinkNode {&nbsp;</div><div>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &nbsp; &nbsp;&nbsp;&nbsp;&nbsp;TreeLinkNode *left;&nbsp;</div><div>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TreeLinkNode *right;&nbsp;</div><div>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TreeLinkNode *next;&nbsp;</div><div>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &nbsp;}&nbsp;</div><div><br></div><div>Populate each next pointer to point to its next right node. If there is no next right node, the next pointer should be set to NULL.&nbsp;</div><div><span style="line-height: 1.42857143;">Initially, all next pointers are set to NULL.&nbsp;</span></div><div><span style="line-height: 1.42857143;"><br></span></div><div><span style="line-height: 1.42857143;">Note:&nbsp;</span></div><div><span style="line-height: 1.42857143;">You may only use constant extra space.&nbsp;</span></div><div><span style="line-height: 1.42857143;">You may assume that it is a perfect binary tree (ie, all leaves are at the same level, and every parent has two children).&nbsp;</span></div><div><span style="line-height: 1.42857143;"><br></span></div><div><span style="line-height: 1.42857143;">For example,&nbsp;</span></div><div><span style="line-height: 1.42857143;">Given the following perfect binary tree,&nbsp;</span></div><div><span style="line-height: 1.42857143;">&nbsp; &nbsp; &nbsp; 1&nbsp;</span></div><div><span style="line-height: 1.42857143;">&nbsp; &nbsp; / &nbsp; &nbsp;\&nbsp;</span></div><div><span style="line-height: 1.42857143;">&nbsp; 2 &nbsp; &nbsp; &nbsp;3&nbsp;</span></div><div><span style="line-height: 1.42857143;">&nbsp;/ \ &nbsp; &nbsp; / \&nbsp;</span></div><div><span style="line-height: 1.42857143;">4 &nbsp;5 &nbsp;6 &nbsp;7&nbsp;</span></div><div><span style="line-height: 1.42857143;">After calling your function, the tree should look like:&nbsp;</span></div><div><span style="line-height: 1.42857143;"><br></span></div><div><span style="line-height: 1.42857143;">&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; 1 -&gt; NULL&nbsp;</span></div><div><span style="line-height: 1.42857143;">&nbsp; &nbsp; &nbsp; &nbsp;/ &nbsp; &nbsp; &nbsp;\&nbsp;</span></div><div><span style="line-height: 1.42857143;">&nbsp; &nbsp; 2 &nbsp; &nbsp;-&gt; &nbsp;3 -&gt; NULL</span></div><div><span style="line-height: 1.42857143;">&nbsp; / &nbsp; \ &nbsp; &nbsp; &nbsp;/ &nbsp; \&nbsp;</span></div><div><span style="line-height: 1.42857143;">&nbsp;4-&gt;5-&gt;6-&gt;7 -&gt; NULL</span><br></div><div><span style="line-height: 1.42857143;"><br></span></div><div><span style="color: rgb(102, 110, 112); font-family: 'Open Sans', Arial, sans-serif; line-height: 22.3999996185303px;">详细题解请见九章算法微博：</span><font color="#666e70" face="Open Sans, Arial, sans-serif"><span style="line-height: 22.3999996185303px;"><a href="http://weibo.com/3948019741/BsKGT8TXu" target="_blank">http://weibo.com/3948019741/BsKGT8TXu</a></span></font><span style="line-height: 1.42857143;"><br></span></div>
```java
public class Solution {
    public void connect(TreeLinkNode root) {
        if (root == null) {
            return;
        }

        TreeLinkNode parent = root;
        TreeLinkNode next = parent.left;
        while (parent != null && next != null) {
            TreeLinkNode prev = null;
            while (parent != null) {
                if (prev == null) {
                    prev = parent.left;
                } else {
                    prev.next = parent.left;
                    prev = prev.next;
                }
                prev.next = parent.right;
                prev = prev.next;
                parent = parent.next;
            }
            parent = next;
            next = parent.left;
        }
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)