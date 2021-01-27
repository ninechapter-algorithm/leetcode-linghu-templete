# 凸多边形
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/convex-polygon/?utm_source=sc-github-wzz)
 ## 题目描述
 给定一组点的数组，当一个多边形按顺序连接时，发现这个多边形是凸多边形([凸多边形定义](https://en.wikipedia.org/wiki/Convex_polygon))。
 ### 样例说明
 ```
样例 1:
	输入: points = [[0, 0], [0, 1], [1, 1], [1, 0]]
	输出:  true
	
	解释:
```
![](https://lintcode-media.s3.amazonaws.com/problem/E3N5G.png)

```
样例 2:
	输入:  points = [[0, 0], [0, 10], [10, 10], [10, 0], [5, 5]]
	输出:  false
	
	解释:
```	
![](https://lintcode-media.s3.amazonaws.com/problem/E3f02.png)
 ### 参考代码
 利用向量外积来判断两个向量的夹角是否是非钝角。
$a 叉乘 b = a和b的模乘夹角的正弦$， 因此结果的正负对应着夹角的大小。
```java
public class Solution {
    public int Cross_Product(List<Integer> p1,List<Integer> p2,List<Integer> p3){
        int ax = p2.get(0) - p1.get(0);
        int ay = p2.get(1) - p1.get(1);
        int bx = p3.get(0) - p2.get(0);
        int by = p3.get(1) - p2.get(1);
        int cp= ax * by - ay * bx;
        if(cp > 0){
            return 1;
        } else if(cp < 0){
            return -1;
        } else {
            return 0;
        }
    }
    public boolean isConvex(List<List<Integer>> points) {
        int cp;
        int numPoints = points.size();
        boolean negativeFlag = false;
        boolean postiveFlag = false;
        for(int i = 2; i < numPoints + 2; i++){
            cp = Cross_Product(points.get((i - 2) % numPoints), points.get((i - 1) % numPoints), points.get(i % numPoints));
            if(cp == 1){
                postiveFlag = true;
            } else if(cp == -1){
                negativeFlag = true;
            } 
        }
        if(postiveFlag && negativeFlag || (!postiveFlag && !negativeFlag)){
            return false;
        } else {
            return true;
        }
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)