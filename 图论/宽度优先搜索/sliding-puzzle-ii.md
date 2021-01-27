# 滑动拼图 II
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/sliding-puzzle-ii/?utm_source=sc-github-wzz)
 ## 题目描述
 在一个3x3的网格中，放着编号1到8的8块板，以及一块编号为0的空格。
一次**移动**可以把空格0与上下左右四邻接之一的板子交换。
给定初始和目标的板子排布，返回到目标排布最少的移动次数。
如果不能从初始排布移动到目标排布，返回-1.
 ### 样例说明
 **样例1 ：**
```
输入:
[
 [2,8,3],
 [1,0,4],
 [7,6,5]
]
[
 [1,2,3],
 [8,0,4],
 [7,6,5]
]
输出:
4

解释:
[                 [
 [2,8,3],          [2,0,3],
 [1,0,4],   -->    [1,8,4],
 [7,6,5]           [7,6,5]
]                 ]

[                 [
 [2,0,3],          [0,2,3],
 [1,8,4],   -->    [1,8,4],
 [7,6,5]           [7,6,5]
]                 ]

[                 [
 [0,2,3],          [1,2,3],
 [1,8,4],   -->    [0,8,4],
 [7,6,5]           [7,6,5]
]                 ]

[                 [
 [1,2,3],          [1,2,3],
 [0,8,4],   -->    [8,0,4],
 [7,6,5]           [7,6,5]
]                 ]
```

**样例 2：**
```
输入:
[[2,3,8],[7,0,5],[1,6,4]]
[[1,2,3],[8,0,4],[7,6,5]]
输出:
-1
```
 ### 参考代码
 使用单向 BFS 算法
```
[[java]]
public class Solution {
    /**
     * @param init_state: the initial state of chessboard
     * @param final_state: the final state of chessboard
     * @return: return an integer, denote the number of minimum moving
     */
    public int minMoveStep(int[][] init_state, int[][] final_state) {
        String source = matrixToString(init_state);
        String target = matrixToString(final_state);
        
        Queue<String> queue = new LinkedList<>();
        Map<String, Integer> distance = new HashMap<>();
        
        queue.offer(source);
        distance.put(source, 0);
        
        while (!queue.isEmpty()) {
            String curt = queue.poll();
            if (curt.equals(target)) {
                return distance.get(curt);
            }
            
            for (String next : getNext(curt)) {
                if (distance.containsKey(next)) {
                    continue;
                }
                queue.offer(next);
                distance.put(next, distance.get(curt) + 1);
            }
        }
        
        return -1;
    }
    
    public String matrixToString(int[][] state) {
        StringBuilder sb = new StringBuilder();
        for (int i = 0; i < 3; i++) {
            for (int j = 0; j < 3; j++) {
                sb.append(state[i][j]);
            }
        }
        return sb.toString();
    }
    
    public List<String> getNext(String state) {
        List<String> states = new ArrayList<>();
        int[] dx = {0, 1, -1, 0};
        int[] dy = {1, 0, 0, -1};
        
        int zeroIndex = state.indexOf('0');
        int x = zeroIndex / 3;
        int y = zeroIndex % 3;
        
        for (int i = 0; i < 4; i++) {
            int x_ = x + dx[i];
            int y_ = y + dy[i];
            if (x_ < 0 || x_ >= 3 || y_ < 0 || y_ >= 3) {
                continue;
            }
            
            char[] chars = state.toCharArray();
            chars[x * 3 + y] = chars[x_ * 3 + y_];
            chars[x_ * 3 + y_] = '0';
            states.add(new String(chars));
        }
        
        return states;
    }
}
[[python]]
class Solution:
    def get_next(self, state):
        states = []
        dirction = ((0, 1), (1, 0), (-1, 0), (0, -1))
        
        zero_index = state.find('0')
        x, y = zero_index // 3, zero_index % 3
        
        for i in range(4):
            x_, y_ = x + dirction[i][0], y + dirction[i][1]
            if 0 <= x_ < 3 and 0 <= y_ < 3:
                next_state = list(state)
                next_state[x * 3 + y] = next_state[x_ * 3 + y_]
                next_state[x_ * 3 + y_] = '0'
                states.append("".join(next_state))
        return states
    
    def minMoveStep(self, init_state, final_state):
        source = self.matrix_to_string(init_state)
        target = self.matrix_to_string(final_state)

        from collections import deque
        queue = deque([source])
        distance = {source: 0}
        
        while queue:
            curt = queue.popleft()
            if curt == target:
                return distance[curt]
                
            for next in self.get_next(curt):
                if next in distance:
                    continue
                
                queue.append(next)
                distance[next] = distance[curt] + 1
        
        return -1
        
    def matrix_to_string(self, state):
        str_list = []
        for i in range(3):
            for j in range(3):
                str_list.append(str(state[i][j]))
        return "".join(str_list)
```

使用双向 BFS 算法。可以把这份代码当模板背诵。

```
[[java]]
public class Solution {
    /**
     * @param init_state: the initial state of chessboard
     * @param final_state: the final state of chessboard
     * @return: return an integer, denote the number of minimum moving
     */
    public int minMoveStep(int[][] init_state, int[][] final_state) {
        String source = matrixToString(init_state);
        String target = matrixToString(final_state);
        
        if (source.equals(target)) {
            return 0;
        }
        
        Queue<String> forwardQueue = new ArrayDeque<>();
        Set<String> forwardSet = new HashSet<>();
        forwardQueue.offer(source);
        forwardSet.add(source);

        Queue<String> backwardQueue = new ArrayDeque<>();
        Set<String> backwardSet = new HashSet<>();
        backwardQueue.offer(target);
        backwardSet.add(target);
        
        int steps = 0;
        while (!forwardQueue.isEmpty() && !backwardQueue.isEmpty()) {
            steps++;
            if (extendQueue(forwardQueue, forwardSet, backwardSet)) {
                return steps;
            }
            
            steps++;
            if (extendQueue(backwardQueue, backwardSet, forwardSet)) {
                return steps;
            }
        }
        
        return -1;
    }
    
    private boolean extendQueue(Queue<String> queue,
                                Set<String> set,
                                Set<String> targetSet) {
        int size = queue.size();
        for (int i = 0; i < size; i++) {
            String curt = queue.poll();
            for (String next : getNext(curt)) {
                if (set.contains(next)) {
                    continue;
                }
                if (targetSet.contains(next)) {
                    return true;
                }
                queue.offer(next);
                set.add(next);
            }
        }
        return false;
    }
    
    public String matrixToString(int[][] state) {
        StringBuilder sb = new StringBuilder();
        for (int i = 0; i < 3; i++) {
            for (int j = 0; j < 3; j++) {
                sb.append(state[i][j]);
            }
        }
        return sb.toString();
    }
    
    public List<String> getNext(String state) {
        List<String> states = new ArrayList<>();
        int[] dx = {0, 1, -1, 0};
        int[] dy = {1, 0, 0, -1};
        
        int zeroIndex = state.indexOf('0');
        int x = zeroIndex / 3;
        int y = zeroIndex % 3;
        
        for (int i = 0; i < 4; i++) {
            int x_ = x + dx[i];
            int y_ = y + dy[i];
            if (x_ < 0 || x_ >= 3 || y_ < 0 || y_ >= 3) {
                continue;
            }
            
            char[] chars = state.toCharArray();
            chars[x * 3 + y] = chars[x_ * 3 + y_];
            chars[x_ * 3 + y_] = '0';
            states.add(new String(chars));
        }
        
        return states;
    }
}
[[python]]
class Solution:
    
    def minMoveStep(self, init_state, final_state):
        source = self.matrix_to_string(init_state)
        target = self.matrix_to_string(final_state)

        from collections import deque
        forward_queue = deque([source])
        forward_set = set([source])
        
        backward_queue = deque([target])
        backward_set = set([target])
        
        steps = 0
        while forward_queue and backward_queue:
            steps += 1
            if self.extend_queue(forward_queue, forward_set, backward_set):
                return steps
                
            steps += 1
            if self.extend_queue(backward_queue, backward_set, forward_set):
                return steps
        
        return -1
        
    def extend_queue(self, queue, source_set, target_set):
        for i in range(len(queue)):
            curt = queue.popleft()
            for next in self.get_next(curt):
                if next in source_set:
                    continue
                if next in target_set:
                    return True
                queue.append(next)
                source_set.add(next)
                
        return False
    
    def matrix_to_string(self, state):
        str_list = []
        for i in range(3):
            for j in range(3):
                str_list.append(str(state[i][j]))
        return "".join(str_list)
        
    def get_next(self, state):
        states = []
        dirction = ((0, 1), (1, 0), (-1, 0), (0, -1))
        
        zero_index = state.find('0')
        x, y = zero_index // 3, zero_index % 3
        
        for i in range(4):
            x_, y_ = x + dirction[i][0], y + dirction[i][1]
            if 0 <= x_ < 3 and 0 <= y_ < 3:
                next_state = list(state)
                next_state[x * 3 + y] = next_state[x_ * 3 + y_]
                next_state[x_ * 3 + y_] = '0'
                states.append("".join(next_state))
        return states
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)