# 填充每个结点的右结点指针II
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/populating-next-right-pointers-in-each-node-ii/?utm_source=sc-github-wzz)
 ## 题目描述
 <p>给定一棵二叉树：</p><pre>    struct TreeLinkNode {
      TreeLinkNode *left;
      TreeLinkNode *right;
      TreeLinkNode *next;
    }</pre><p>填充每个结点指向其同层右边下一个结点的指针next。如果右边没有下一个结点，则next指针指向NULL。</p><p>初始时，所有的next指针全部指向NULL。</p>
 ### 样例说明
 
 ### 参考代码
 Follow up for problem "Populating Next Right Pointers in Each Node".&nbsp;<div>What if the given tree could be any binary tree? Would your previous solution still work?&nbsp;</div><div>Note:&nbsp;<span style="line-height: 1.42857143;">&nbsp;You may only use constant extra space.&nbsp;</span></div><div><span style="line-height: 1.42857143;"><br></span></div><div><span style="line-height: 1.42857143;">For example,&nbsp;</span></div><div><span style="line-height: 1.42857143;">Given the following binary tree,&nbsp;</span></div><div><span style="line-height: 1.42857143;">&nbsp; &nbsp; &nbsp; 1&nbsp;</span></div><div><span style="line-height: 1.42857143;">&nbsp; &nbsp; &nbsp;/  \&nbsp;</span></div><div><span style="line-height: 1.42857143;">&nbsp; &nbsp;2 &nbsp; 3&nbsp;</span></div><div><span style="line-height: 1.42857143;">&nbsp; / \ &nbsp; &nbsp;\&nbsp;</span></div><div><span style="line-height: 1.42857143;">&nbsp;4 &nbsp;5 &nbsp; &nbsp;7&nbsp;</span></div><div><span style="line-height: 1.42857143;">After calling your function, the tree should look like:&nbsp;</span></div><div><span style="line-height: 1.42857143;">&nbsp; &nbsp; &nbsp; &nbsp; 1 -&gt; NULL</span></div><div><span style="line-height: 1.42857143;">&nbsp; &nbsp; &nbsp; / &nbsp; &nbsp;\&nbsp;</span></div><div><span style="line-height: 1.42857143;">&nbsp; &nbsp; 2 &nbsp;-&gt; 3 -&gt; NULL&nbsp;</span></div><div><span style="line-height: 1.42857143;">&nbsp; / &nbsp; &nbsp;\ &nbsp; &nbsp; &nbsp;\&nbsp;</span></div><div><span style="line-height: 1.42857143;">&nbsp;4-&gt; 5 -&gt; 7 -&gt; NULL</span></div><div><span style="line-height: 1.42857143;"><br></span></div><div><span style="color: rgb(102, 110, 112); font-family: 'Open Sans', Arial, sans-serif; line-height: 22.3999996185303px;">详细题解请见九章算法微博：</span><font color="#666e70" face="Open Sans, Arial, sans-serif"><span style="line-height: 22.3999996185303px;"><a href="http://weibo.com/3948019741/BsC0Q9jY7" target="_blank">http://weibo.com/3948019741/BsC0Q9jY7</a></span></font><span style="line-height: 1.42857143;"><br></span></div>
```java
public class Solution {
    public void connect(TreeLinkNode root) {
        if (root == null) {
            return;
        }

        TreeLinkNode parent = root;
        TreeLinkNode pre;
        TreeLinkNode next;
        while (parent != null) {
            pre = null;
            next = null;
            while (parent != null) {
                if (next == null){
                    next = (parent.left != null) ? parent.left: parent.right;
                }

                if (parent.left != null){
                    if (pre != null) {
                        pre.next = parent.left;
                        pre = pre.next;
                    } else {
                        pre = parent.left;
                    }
                }

                if (parent.right != null) {
                    if (pre != null) {
                        pre.next = parent.right;
                        pre = pre.next;
                    } else {
                        pre = parent.right;
                    }
                }
                parent = parent.next;
            }
            parent = next;
        }
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)