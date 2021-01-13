# 区间求和  I
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/interval-sum/?utm_source=sc-github-wzz)
 ## 题目描述
 给定一个整数数组（下标由 0 到 n-1，其中 n 表示数组的规模），以及一个查询列表。每一个查询列表有两个整数 `[start, end]` 。 对于每个查询，计算出数组中从下标 start 到 end 之间的数的总和，并返回在结果列表中。 
 ### 样例说明
 **样例 1:**
```
输入: 数组 = [1,2,7,8,5], 查询 = [(0,4),(1,2),(2,4)]
输出: [23,9,20]
```

**样例 2:**
```
输入: 数组 = [4,3,1,2],  查询 = [(1,2),(0,2)]
输出: [4,8]
```
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
public class Solution {
    /**
     *@param A, queries: Given an integer array and an query list
     *@return: The result list
     */
     class SegmentTreeNode {
        public int start, end;
        public Long sum;
        public SegmentTreeNode left, right;
        public SegmentTreeNode(int start, int end, Long sum) {
              this.start = start;
              this.end = end;
              this.sum = sum;
              this.left = this.right = null;
        }
    }
    public SegmentTreeNode build(int start, int end, int[] A) {
        // write your code here
        if(start > end) {  // check core case
            return null;
        }
        
        SegmentTreeNode root = new SegmentTreeNode(start, end, 0L);
        
        if(start != end) {
            int mid = (start + end) / 2;
            root.left = build(start, mid, A);
            root.right = build(mid+1, end, A);
            
            root.sum = root.left.sum + root.right.sum;
        } else {
            root.sum =  Long.valueOf(A[start]);
            
        }
        return root;
    }
    public Long query(SegmentTreeNode root, int start, int end) {
        // write your code here
        if(start == root.start && root.end == end) { // 相等 
            return root.sum;
        }
        
        
        int mid = (root.start + root.end)/2;
        Long leftsum = 0L, rightsum = 0L;
        // 左子区
        if(start <= mid) {
            if( mid < end) { // 分裂 
                leftsum =  query(root.left, start, mid);
            } else { // 包含 
                leftsum = query(root.left, start, end);
            }
        }
        // 右子区
        if(mid < end) { // 分裂 3
            if(start <= mid) {
                rightsum = query(root.right, mid+1, end);
            } else { //  包含 
                rightsum = query(root.right, start, end);
            } 
        }  
        // else 就是不相交
        return leftsum + rightsum;
    }
    public ArrayList<Long> intervalSum(int[] A, 
                                       ArrayList<Interval> queries) {
        // write your code here
        SegmentTreeNode root = build(0, A.length - 1, A);
        ArrayList ans = new ArrayList<Long>();
        for(Interval in : queries) {
            ans.add(query(root, in.start, in.end));
        }
        return ans;
    }
}


 *     Interval(int start, int end) {
 *         this.start = start;
 *         this.end = end;
 *     }
 */

public class Solution {
    /**
     *@param A, queries: Given an integer array and an query list
     *@return: The result list
     */
    public class SegmentTreeNode {
        public int start, end, min;
        public SegmentTreeNode left, right;
        public SegmentTreeNode(int start, int end, int min) {
              this.start = start;
              this.end = end;
              this.min = min;
              this.left = this.right = null;
        }
    }
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
        if(start == root.start && root.end == end) { // equal
            return root.min;
        }
       
       
        int mid = (root.start + root.end)/2;
        int leftmin = Integer.MAX_VALUE, rightmin = Integer.MAX_VALUE;
        // left
        if(start <= mid) {
            if( mid < end) { // split
                leftmin =  query(root.left, start, mid);
            } else { //  contain
                leftmin = query(root.left, start, end);
            }
        }
        // right
        if(mid < end) { // split
            if(start <= mid) {
                rightmin = query(root.right, mid+1, end);
            } else { //  contain
                rightmin = query(root.right, start, end);
            }
        }
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