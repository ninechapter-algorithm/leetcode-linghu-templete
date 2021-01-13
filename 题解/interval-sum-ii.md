# 区间求和 II
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/interval-sum-ii/?utm_source=sc-github-wzz)
 ## 题目描述
 在类的构造函数中给一个整数数组, 实现两个方法 `query(start, end)` 和 `modify(index, value)`:

- 对于 query(*start*, *end*), 返回数组中下标 *start* 到 *end* 的 **和**。
- 对于 modify(*index*, *value*), 修改数组中下标为 *index* 上的数为 *value*.
 ### 样例说明
 **样例1**

```plain
输入:
[1,2,7,8,5]
[query(0,2),modify(0,4),query(0,1),modify(2,1),query(2,4)]
输出: [10,6,14]
说明:
给定数组 A = [1,2,7,8,5].
在query(0, 2)后, 1 + 2 + 7 = 10,
在modify(0, 4)后, 将 A[0] 修改为 4， A = [4,2,7,8,5].
在query(0, 1)后, 4 + 2 = 6.
在modify(2, 1)后, 将 A[2] 修改为 1，A = [4,2,1,8,5].
After query(2, 4), 1 + 8 + 5 = 14.
```

**样例2**

```plain
输入:
[1,2,3,4,5]
[query(0,0),query(1,2),quert(3,4)]
输出: [1,5,9]
说明:
1 = 1
2 + 3 = 5
4 + 5 = 9
```


 ### 参考代码
 本题为线段树的基本运用，实现线段树的修改和查询即可。
```java
public class Solution {
    /* you may need to use some attributes here */
    
     class SegmentTreeNode {
        public int start, end;
        public int sum;
        public SegmentTreeNode left, right;
        public SegmentTreeNode(int start, int end, int sum) {
              this.start = start;
              this.end = end;
              this.sum = sum;
              this.left = this.right = null;
        }
    }
    SegmentTreeNode root;
    public SegmentTreeNode build(int start, int end, int[] A) {
        // write your code here
        if(start > end) {  // check core case
            return null;
        }
        
        SegmentTreeNode root = new SegmentTreeNode(start, end, 0);
        
        if(start != end) {
            int mid = (start + end) / 2;
            root.left = build(start, mid, A);
            root.right = build(mid+1, end, A);
            
            root.sum = root.left.sum + root.right.sum;
        } else {
            root.sum =  A[start];
            
        }
        return root;
    }
    public int querySegmentTree(SegmentTreeNode root, int start, int end) {
        // write your code here
        if(start == root.start && root.end == end) { // 相等 
            return root.sum;
        }
        
        
        int mid = (root.start + root.end)/2;
        int leftsum = 0, rightsum = 0;
        // 左子区
        if(start <= mid) {
            if( mid < end) { // 分裂 
                leftsum =  querySegmentTree(root.left, start, mid);
            } else { // 包含 
                leftsum = querySegmentTree(root.left, start, end);
            }
        }
        // 右子区
        if(mid < end) { // 分裂 3
            if(start <= mid) {
                rightsum = querySegmentTree(root.right, mid+1, end);
            } else { //  包含 
                rightsum = querySegmentTree(root.right, start, end);
            } 
        }  
        // else 就是不相交
        return leftsum + rightsum;
    }
    public void modifySegmentTree(SegmentTreeNode root, int index, int value) {
        // write your code here
        if(root.start == index && root.end == index) { // 查找到
            root.sum = value;
            return;
        }
        
        // 查询
        int mid = (root.start + root.end) / 2;
        if(root.start <= index && index <=mid) {
            modifySegmentTree(root.left, index, value);
        }
        
        if(mid < index && index <= root.end) {
            modifySegmentTree(root.right, index, value);
        }
        //更新
        root.sum = root.left.sum + root.right.sum;
    }
    /**
     * @param A: An integer array
     */
    public Solution(int[] A) {
        // write your code here
        root = build(0, A.length-1, A);
    }
    
    /**
     * @param start, end: Indices
     * @return: The sum from start to end
     */
    public long query(int start, int end) {
        // write your code here
        return querySegmentTree(root, start ,end);
    }
    
    /**
     * @param index, value: modify A[index] to value.
     */
    public void modify(int index, int value) {
        // write your code here
        modifySegmentTree(root, index, value);
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)