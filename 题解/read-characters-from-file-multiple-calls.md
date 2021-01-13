# read characters from file multiple calls
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/read-characters-from-file-multiple-calls/?utm_source=sc-github-wzz)
 ## 题目描述
 1781
 ### 样例说明
 1781
 ### 参考代码
 ```cpp
// version 1
// Forward declaration of the read4 API.
int read4(char *buf);

class Solution {
public:
  /**
   * @param buf Destination buffer
   * @param n   Maximum number of characters to read
   * @return  The number of characters read
   */
  char buffer[4];
  int bufferPtr = 0, bufferCnt = 0;
  
  int read(char *buf, int n) {
    // Write your code here
    int ptr = 0;

    while (ptr < n) {
      if (bufferPtr == bufferCnt) {
        bufferCnt = read4(buffer);
        bufferPtr = 0;
      }
      if (bufferCnt == 0) {
        break;
      }
      while (ptr < n && bufferPtr < bufferCnt) {  
        buf[ptr++] = buffer[bufferPtr++];
      }
    } 
    return ptr;
  }
};

// version 2
// Forward declaration of the read4 API.
int read4(char *buf);

class Solution {
public:
    /**
     * @param buf destination buffer
     * @param n maximum number of characters to read
     * @return the number of characters read
     */
    int read(char *buf, int n) {
        // Write your code here
        int i = 0;
        while (i < n && (i4 < n4 || (i4 = 0) < (n4 = read4(buf4))))
            buf[i++] = buf4[i4++];
        return i;
    }
    char buf4[4];
    int i4 = 0, n4 = 0;
};
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)