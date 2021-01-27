# 2D战舰
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/battleships-in-a-board/?utm_source=sc-github-wzz)
 ## 题目描述
 给一个 2D 板, 计数上面有多少战舰. 战舰用 `'X'` 表示，空地用 `'.'` 表示。你可以假设有一下规则：
* 你会得到一个有效的板，上面只有战舰跟空地。
* 战舰只能横着或者竖着放。换句话说，它们的大小只能是  `1xN` (1 行, N 列) 或者 `Nx1` (N 行, 1 列), N 可以是任意数。
* 在两艘战舰之间至少有一个横向的或者纵向的格子分隔 - 没有相邻的战舰
 ### 样例说明
 **样例1**
```
输入：
X..X
...X
...X
输出： 2
解释：
在上述板上有两艘战舰。
```
**样例2**
```
输入：
...X
XXXX
...X
解释：
这是一个你不会得到的无效输入 - 因为战舰之间始终会有一个单元格分隔。
```

 ### 参考代码
 我们发现对于船头，他的左边和上面一定为空地（或边界），因此只需要统计船头的个数即可知道战舰的个数。
```java
// 方法一
public class Solution {
    public int countBattleships(char[][] board) {
        int len1 = board.length;
        if(len1 == 0){
            return 0;
        }
        int len2 = board[0].length;
        int ans = 0;
        for (int i = 0; i < len1; i++){
            for(int j=0 ; j < len2; j++){
                if(board[i][j] == 'X' && (i == 0 || board[i-1][j] == '.') && (j == 0 || board[i][j-1] == '.')){
                    ans ++;
                }
            }
        }
        return ans;
    }
}

// 方法二
class Solution {
public:
    int countBattleships(vector<vector<char>>& board) {
        int len1 = board.size();
        if(len1 == 0) {
            return 0;
        }
        int len2 = board[0].size();
        int ans = 0;
        int dx[4] = {0,0,-1,1};
        int dy[4] = {-1,1,0,0};
        for(int i=0; i < len1; i++){
            for(int j =0; j < len2; j++){
                if(board[i][j] == 'X'){
                    board[i][j] = '.';//标记已经访问过
                    ans++;
                    int pos1 = i;
                    int pos2 = j;
                    for(int k =0; k < 4; k++){
                        //一直沿着同一个方向搜索
                        while(pos1+dx[k] >=0 && pos1+dx[k] < len1 && pos2 + dy[k] >=0 && pos2+dy[k]<len2 && board[pos1+[k]][pos2+dy[k]] == 'X'){
                                board[pos1+dx[k]][pos2+dy[k]] = '.';
                                pos1 += dx[k];
                                pos2 += dy[k];
                            }
                    }
                }
            }
        }
        return ans;
    }
};
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)