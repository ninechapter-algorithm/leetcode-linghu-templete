# 奇偶跳
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/odd-even-jump/?utm_source=sc-github-wzz)
 ## 题目描述
 给定一个整数数组A。从某一些起始索引，你可以做一系列的跳跃。`其中的（第1，第3，第5 ......）跳跃称为奇数跳跃，（第2，第4，第6 ......）跳跃称为偶数跳跃`。

你可以从索引` i ` 以下列方式跳转到索引 `j`（i <j）：

在奇数跳跃（即跳跃1,3,5，...）期间，跳转到索引j，使得`A [i] <= A [j]`并且A [j]是可能的最小值。如果有多个这样的索引j，则只能跳转到最小的索引 j。 在偶数跳跃（即跳跃2,4,6，...）期间，跳转到索引j，使得`A [i]> = A [j]`，A [j]是最大的可能值。如果有多个这样的索引j，则只能跳转到最小的索引 j。（可能存在某些索引，不存在合法的跳跃）
如果从该索引开始，您可以通过跳转一些次数（大于等于0次）到达数组的末尾（索引A.length - 1），那么这是一个有效的起始索引。

返回有效的起始索引的个数

 ### 样例说明
 **样例 1:**
```
输入: [10,13,12,14,15]
输出: 2
解析: 
从 index i = 0 开始，我们可以跳跃至 i = 2 (因为 A[2] 是 A[1], A[2], A[3], A[4] 中 >= A[0]最小的), 然后我们就无法再继续跳跃了
从 i = 1 和 i = 2 开始, 我们可以跳跃至 i = 3, 然后无法再继续跳跃了
从 i = 3 开始, 我们可以跳跃至 i = 4, 因此我们可以到达末尾
从 i = 4 开始, 我们已经在末尾了
综上, 有 2 个有效的索引 (i = 3, i = 4) 我们可以经过一系列的跳跃达到末尾
```
**样例 2:**
```
输入: [2,3,1,1,4]
输出: 3
解析: 
从 i = 0 开始, 我们可以跳跃至 i = 1, i = 2, i = 3:

在我们的第一次跳跃 (奇数跳), 我们先跳跃至 i = 1, 因为 A[1] 是 (A[1], A[2], A[3], A[4] >= A[0]) 当中最小的，

在我们的第二次跳跃 (偶数跳), 我们从 i = 1 跳到 i = 2 因为 A[2] 是 (A[2], A[3], A[4] <= A[1])当中最大的.  A[3] 也是最大的, 但是 2 是更小的索引, 所以我们跳到 i = 2 而不是 i = 3.

在我们的第三次跳跃 (奇数跳),我们从 i = 2 跳到 i = 3 因为 A[3] 是 (A[3], A[4] >= A[2])当中最小的

我们不能从 i = 3 跳跃 i = 4, 因此起始索引 i = 0 是无效的

根据同样的规则，我们可以求出：
存在 3 个有效的起始索引 (i = 1, i = 3, i = 4) 我们可以跳跃至末尾
```
 ### 参考代码
 线段树建图+动态规划解法
```
[[python]]
def get_max(pair_a, pair_b):
    if pair_a[0] != pair_b[0]:
        return max(pair_a, pair_b)
    if pair_a[1] < pair_b[1]:
        return pair_a
    return pair_b
    
def get_min(pair_a, pair_b):
    if pair_a[0] != pair_b[0]:
        return min(pair_a, pair_b)
    if pair_a[1] < pair_b[1]:
        return pair_a
    return pair_b

class MySegmentTreeNode:
    
    def __init__(self, start, end):
        self.start, self.end = start, end
        self.max_val, self.min_val = (-float('inf'), -1), (float('inf'), -1)
        self.left_child, self.right_child = None, None
    
    
class MySegmentTree:
    
    def __init__(self, start, end):
        self.range_start = start
        self.range_end = end
        self.root = self.build_tree(start, end)
    
    def build_tree(self, start, end):
        node = MySegmentTreeNode(start, end)
        if start == end:
            return node
            
        node.left_child = self.build_tree(start, (start + end) // 2)
        node.right_child = self.build_tree((start + end ) // 2 + 1, end)
        return node
    
    def insert(self, index, val, node=None):
        if node is None:
            node = self.root
        if node.start == index and node.end == index:
            node.max_val = node.min_val = val
            return
        if index <= node.left_child.end:
            self.insert(index, val, node.left_child)
        else:
            self.insert(index, val, node.right_child)
        node.max_val = get_max(node.left_child.max_val, node.right_child.max_val)
        node.min_val = get_min(node.left_child.min_val, node.right_child.min_val)
    
    def query_max(self, start, end, node=None):
        if node is None:
            node = self.root
        if end < start:
            return (-float('inf'), -1)
        if node.start == start and node.end == end:
            return node.max_val
        if end <= node.left_child.end:
            return self.query_max(start, end, node.left_child)
        elif start >= node.right_child.start:
            return self.query_max(start, end, node.right_child)
        return get_max(
            self.query_max(start, node.left_child.end, node.left_child),
            self.query_max(node.right_child.start, end, node.right_child)
        )
        
    def query_min(self, start, end, node=None):
        if node is None:
            node = self.root
        if end < start:
            return (float('inf'), -1)
        if node.start == start and node.end == end:
            return node.min_val
        if end <= node.left_child.end:
            return self.query_min(start, end, node.left_child)
        elif start >= node.right_child.start:
            return self.query_min(start, end, node.right_child)
        return get_min(
            self.query_min(start, node.left_child.end, node.left_child),
            self.query_min(node.right_child.start, end, node.right_child)
        )


class Solution:
    """
    @param A: An integer array A
    @return: Return the number of good starting indexes
    """
    def oddEvenJumps(self, A):
        odd_jump, even_jump = self.get_jumps(A)

        # dp = array of n x 2
        # dp[i][0] can we jump to n - 1 when we arrive i by even jumps
        # dp[i][1] can we jump to n - 1 when we arrive i by odd jumps
        n = len(A)
        dp = [[False, False] for _ in range(n)]
        dp[n - 1][0] = dp[n - 1][1] = True
        
        answer = 1
        for i in range(n - 2, -1, -1):
            dp[i][0] = dp[odd_jump[i]][1] if odd_jump[i] != -1 else False
            dp[i][1] = dp[even_jump[i]][0] if even_jump[i] != -1 else False
            if dp[i][0] == True:
                answer += 1
        return answer
        
    def get_jumps(self, A):
        import bisect
        sorted_A = sorted(list(set(A)))
        range_start = bisect.bisect(sorted_A, min(A))
        range_end = bisect.bisect(sorted_A, max(A))
        seg = MySegmentTree(range_start, range_end)

        n = len(A)
        even_jump = [-1] * n
        odd_jump = [-1] * n
        for i in range(n - 1, -1, -1):
            val = bisect.bisect(sorted_A, A[i])
            odd_jump[i] = seg.query_min(val, range_end)[1]
            even_jump[i] = seg.query_max(range_start, val)[1]
            seg.insert(val, (val, i))
            
        return odd_jump, even_jump
[[java]]
class Pair {
    int value, index;
    
    Pair(int value, int index) {
        this.value = value;
        this.index = index;
    }
}

class MySegmentTreeNode {
    int start, end;
    Pair maxValue, minValue;
    MySegmentTreeNode leftChild, rightChild;
    
    MySegmentTreeNode(int start, int end) {
        this.start = start;
        this.end = end;
        this.maxValue = new Pair(Integer.MIN_VALUE, -1);
        this.minValue = new Pair(Integer.MAX_VALUE, -1);
        this.leftChild = this.rightChild = null;
    }
}

class MySegmentTree {
    int rangeStart, rangeEnd;
    MySegmentTreeNode root;
    
    MySegmentTree(int start, int end) {
        rangeStart = start;
        rangeEnd = end;
        root = buildTree(start, end);
    }
    
    private MySegmentTreeNode buildTree(int start, int end) {
        MySegmentTreeNode node = new MySegmentTreeNode(start, end);
        
        if (start == end) {
            return node;
        }
        
        int middle = start + (end - start) / 2;
        node.leftChild = buildTree(start, middle);
        node.rightChild = buildTree(middle + 1, end);
        
        return node;
    }
    
    public void insert(int index, Pair value) {
        insert(index, value, this.root);
    }
    
    private void insert(int index, Pair value, MySegmentTreeNode node) {
        if (node.start == index && node.end == index) {
            node.maxValue = node.minValue = value;
            return;
        }
        if (index <= node.leftChild.end) {
            insert(index, value, node.leftChild);
        } else {
            insert(index, value, node.rightChild);
        }
        
        node.maxValue = getMax(node.leftChild.maxValue, node.rightChild.maxValue);
        node.minValue = getMin(node.leftChild.minValue, node.rightChild.minValue);
    }
    
    public Pair queryMax(int start, int end) {
        return queryMax(start, end, this.root);
    }
    
    private Pair queryMax(int start, int end, MySegmentTreeNode node) {
        if (end < start) {
            return new Pair(Integer.MIN_VALUE, -1);
        }
        if (node.start == start && node.end == end) {
            return node.maxValue;
        }
        
        if (end <= node.leftChild.end) {
            return queryMax(start, end, node.leftChild);
        } else if (start >= node.rightChild.start) {
            return queryMax(start, end, node.rightChild);
        }
        
        return getMax(
            queryMax(start, node.leftChild.end, node.leftChild),
            queryMax(node.rightChild.start, end, node.rightChild)
        );
    }
    
    public Pair queryMin(int start, int end) {
        return queryMin(start, end, this.root);
    }
    
    private Pair queryMin(int start, int end, MySegmentTreeNode node) {
        if (end < start) {
            return new Pair(Integer.MIN_VALUE, -1);
        }
        if (node.start == start && node.end == end) {
            return node.minValue;
        }
        
        if (end <= node.leftChild.end) {
            return queryMin(start, end, node.leftChild);
        } else if (start >= node.rightChild.start) {
            return queryMin(start, end, node.rightChild);
        }
        
        return getMin(
            queryMin(start, node.leftChild.end, node.leftChild),
            queryMin(node.rightChild.start, end, node.rightChild)
        );
    }
    
    private static Pair getMax(Pair pairA, Pair pairB) {
        if (pairA.value != pairB.value) {
            return pairA.value > pairB.value ? pairA : pairB;
        }
        
        return pairA.index < pairB.index ? pairA : pairB;
    }
    
    private static Pair getMin(Pair pairA, Pair pairB) {
        if (pairA.value != pairB.value) {
            return pairA.value < pairB.value ? pairA : pairB;
        }
        
        return pairA.index < pairB.index ? pairA : pairB;
    }
}

public class Solution {
    /**
     * @param A: An integer array A
     * @return: Return the number of good starting indexes
     */
    public int oddEvenJumps(int[] A) {
        int n = A.length;
        int[] oddJump = new int[n];
        int[] evenJump = new int[n];
        getJumps(A, oddJump, evenJump);
        
        // dp = array of n x 2
        // dp[i][0] can we jump to n - 1 when we arrive i by even jumps
        // dp[i][1] can we jump to n - 1 when we arrive i by odd jumps
        boolean[][] dp = new boolean[n][2];
        for (int i = 0; i < n; i++) {
            dp[i][0] = false;
            dp[i][1] = false;
        }
        
        dp[n - 1][0] = dp[n - 1][1] = true;
        
        int answer = 1;
        for (int i = n - 2; i >= 0; i--) {
            dp[i][0] = oddJump[i] != -1 ? dp[oddJump[i]][1] : false;
            dp[i][1] = evenJump[i] != -1 ? dp[evenJump[i]][0] : false;
            if (dp[i][0] == true) {
                answer++;
            }
        }
        return answer;
    }
    
    private void getJumps(int[] A, int[] oddJump, int[] evenJump) {
        int n = A.length, count = 0;;
        int[] B = new int[n];
        System.arraycopy(A, 0, B, 0, n);
        Arrays.sort(B);
        Map<Integer, Integer> value2Index = new HashMap<>();
        int minVal = Integer.MAX_VALUE, maxVal = Integer.MIN_VALUE;
        for (int i = 0; i < B.length; i++) {
            if (value2Index.containsKey(B[i])) {
                continue;
            }
            value2Index.put(B[i], ++count);
        }
        
        int rangeStart = 1, rangeEnd = A.length;
        MySegmentTree seg = new MySegmentTree(rangeStart, rangeEnd);
        
        for (int i = 0; i < n; i++) {
            oddJump[i] = -1;
            evenJump[i] = -1;
        }
        
        for (int i = n - 1; i >= 0; i--) {
            int index = value2Index.get(A[i]);
            oddJump[i] = seg.queryMin(index, rangeEnd).index;
            evenJump[i] = seg.queryMax(rangeStart, index).index;
            seg.insert(index, new Pair(index, i));
        }
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)