# 用Read4从文件中读取N个字符 II-多次调用
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/read-n-characters-given-read4-ii-call-multiple-times/?utm_source=sc-github-wzz)
 ## 题目描述
 接口：`int read4(char * buf)`一次从文件中读取 `4` 个字符。
返回值是实际读取的字符数。 例如，如果文件中只剩下 3 个字符，则返回 3。
通过使用read4 接口，实现从文件读取 n 个字符的函数`int read(char * buf，int n)`。
 ### 样例说明
 
 ### 参考代码
 ```java
/* The read4 API is defined in the parent class Reader4.
      int read4(char[] buf); */

public class Solution extends Reader4 {
    private char[] buf4 = new char[4];
    private int buf4Index = 4;
    private int buf4Size = 4;
    
    private boolean readNext(char[] buf, int index) {
        if (buf4Index >= buf4Size) {
            buf4Size = read4(buf4);
            buf4Index = 0;
            if (buf4Size == 0) {
                return false;
            }
        }

        buf[index] = buf4[buf4Index++];
        return true;
    }
    
    /**
     * @param buf Destination buffer
     * @param n   Maximum number of characters to read
     * @return    The number of characters read
     */
    public int read(char[] buf, int n) {
        for (int i = 0; i < n; i++) {
            if (!readNext(buf, i)) {
                return i;
            }
        }
        
        return n;
    }
}


//version:高频题班
public class Solution extends Reader4 {
    /**
     * @param buf destination buffer
     * @param n maximum number of characters to read
     * @return the number of characters read
     */
    char[] buffer = new char[4];
    int head = 0, tail = 0;

    public int read(char[] buf, int n) {
        // Write your code here
        int i = 0;
        while (i < n) {
            if (head == tail) {               // queue is empty
                head = 0;
                tail = read4(buffer);         // enqueue
                if (tail == 0) {
                    break;
                }
            }
            while (i < n && head < tail) {
                buf[i++] = buffer[head++];    // dequeue
            }
        }
        return i;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)