# 区间最小数
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/interval-minimum-number/?utm_source=sc-github-wzz)
 ## 题目描述
 给定一个整数数组（下标由 0 到 n-1，其中 n 表示数组的规模），以及一个查询列表。每一个查询列表有两个整数 `[start, end]`。 对于每个查询，计算出数组中从下标 start 到 end 之间的数的最小值，并返回在结果列表中。 
 ### 样例说明
 **样例1：**
`输入：数组 ：[1,2,7,8,5] 查询 ：[(1,2),(0,4),(2,4)]。输出：[2,1,5]`
**样例2：**
`输入：数组 ：[4,5,7,1] 查询 ：[(1,2),(1,3)]。输出：[5,1]`
 ### 参考代码
 ```java
/**
 * Definition of Interval:
 * public classs Interval {
 *     int start, end;
 *     Interval(int start, int end) {
 *         this.start = start;
 *         this.end = end;
 *     }
 */
class SegmentTreeNode {
    public int start, end, min;
    public SegmentTreeNode left, right;
    public SegmentTreeNode(int start, int end, int min) {
          this.start = start;
          this.end = end;
          this.min = min;
          this.left = this.right = null;
    }
}
public class Solution {
    /**
     *@param A, queries: Given an integer array and an query list
     *@return: The result list
     */
    public SegmentTreeNode build(int start, int end, int[] A) {
        // write your code here
        if(start > end) {  // check core case
            return null;
        }
        
        SegmentTreeNode root = new SegmentTreeNode(start, end, Integer.MAX_VALUE);
        
        if(start != end) {
            int mid = (start + end) / 2;
            root.left = build(start, mid, A);
            root.right = build(mid+1, end, A);
            
            root.min = Math.min(root.left.min, root.right.min);
        } else {
            root.min = A[start];
        }
        return root;
    }
    public int query(SegmentTreeNode root, int start, int end) {
        // write your code here
        if(start == root.start && root.end == end) { // 相等 
            return root.min;
        }
        
        
        int mid = (root.start + root.end)/2;
        int leftmin = Integer.MAX_VALUE, rightmin = Integer.MAX_VALUE;
        // 左子区
        if(start <= mid) {
            if( mid < end) { // 分裂 
                leftmin =  query(root.left, start, mid);
            } else { // 包含 
                leftmin = query(root.left, start, end);
            }
        }
        // 右子区
        if(mid < end) { // 分裂 3
            if(start <= mid) {
                rightmin = query(root.right, mid+1, end);
            } else { //  包含 
                rightmin = query(root.right, start, end);
            } 
        }  
        // else 就是不相交
        return Math.min(leftmin, rightmin);
    }
    
    public List<Integer> intervalMinNumber(int[] A, 
                                           List<Interval> queries) {
        // write your code here
        SegmentTreeNode root = build(0, A.length - 1, A);
        List<Integer> ans = new ArrayList<Integer>();
        for(Interval in : queries) {
            ans.add(query(root, in.start, in.end));
        }
        return ans;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)