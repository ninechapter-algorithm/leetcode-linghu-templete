# 课程表
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/course-schedule/?utm_source=sc-github-wzz)
 ## 题目描述
 现在你总共有 n 门课需要选，记为 `0` 到 `n - 1`.
一些课程在修之前需要先修另外的一些课程，比如要学习课程 0 你需要先学习课程 1 ，表示为[0,1]
给定n门课以及他们的先决条件，判断是否可能完成所有课程？
 ### 样例说明
 例1:
```
输入: n = 2, prerequisites = [[1,0]] 
输出: true
```
例2:
```
输入: n = 2, prerequisites = [[1,0],[0,1]] 
输出: false
```

 ### 参考代码
 裸拓扑排序
```java
public class Solution {
    /**
     * @param numCourses a total of n courses
     * @param prerequisites a list of prerequisite pairs
     * @return true if can finish all courses or false
     */
    public boolean canFinish(int numCourses, int[][] prerequisites) {
        // Write your code here
        List[] edges = new ArrayList[numCourses];
        int[] degree = new int[numCourses];
        
        for (int i = 0;i < numCourses; i++)
            edges[i] = new ArrayList<Integer>();
            
        for (int i = 0; i < prerequisites.length; i++) {
            degree[prerequisites[i][0]] ++ ;
            edges[prerequisites[i][1]].add(prerequisites[i][0]);
        }

        Queue queue = new LinkedList();
        for(int i = 0; i < degree.length; i++){
            if (degree[i] == 0) {
                queue.add(i);
            }
        }
        
        int count = 0;
        while(!queue.isEmpty()){
            int course = (int)queue.poll();
            count ++;
            int n = edges[course].size();
            for(int i = 0; i < n; i++){
                int pointer = (int)edges[course].get(i);
                degree[pointer]--;
                if (degree[pointer] == 0) {
                    queue.add(pointer);
                }
            }
        }
        
        return count == numCourses;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)