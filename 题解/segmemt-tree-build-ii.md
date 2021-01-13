# segmemt-tree-build-ii
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/segmemt-tree-build-ii/?utm_source=sc-github-wzz)
 ## 题目描述
 1763
 ### 样例说明
 1763
 ### 参考代码
 ```java

/**
 * Definition of SegmentTreeNode:
 * public class SegmentTreeNode {
 *     public int start, end, max;
 *     public SegmentTreeNode left, right;
 *     public SegmentTreeNode(int start, int end, int max) {
 *         this.start = start;
 *         this.end = end;
 *         this.max = max
 *         this.left = this.right = null;
 *     }
 * }
 */
public class Solution {
    /**
     *@param A: a list of integer
     *@return: The root of Segment Tree
     */
    public SegmentTreeNode build(int[] A) {
        // write your code here
        return build(0,A.length-1, A);
    }
    
    public SegmentTreeNode build(int start, int end, int[]array) {
        // write your code here
        if(start > end) {  // check core case
            return null;
        }
        
        SegmentTreeNode root = new SegmentTreeNode(start, end, Integer.MIN_VALUE);
        
        if(start != end) {
            int mid = (start + end) / 2;
            root.left = build(start, mid, array);
            root.right = build(mid+1, end, array);
            
            root.max = Math.max(root.left.max, root.right.max);
        } else {
            root.max = array[start];
        }
        return root;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)