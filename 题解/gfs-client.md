# GFS客户端
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/gfs-client/?utm_source=sc-github-wzz)
 ## 题目描述
 为GFS(Google文件系统)实现一个简单的客户端，提供一下功能：
	1.`read(文件名)`，通过文件名从GFS中读取文件。
	2.`write(文件名，内容)`，通过文件名和内容写入GFS中。
现在有两种已经在基础类中实现的方法：
	1.`readChunk(文件名，块索引)`，从GFS中读取一个块。
	2.`writeChunk(文件名，块索引，块数据)`，向GFS中写入一个块。
为了简化这个问题，我们可以假设块大小为 *chunkSize* 位的(在真实的文件系统中，是64M)，GFS客户端的任务是将一个文件分为若干块(如果需要的话)并且保存在远端的GFS服务器上，*chunkSize*会在构造函数中给出，你需要的是实现`read`和`write`这两个private方法。
 ### 样例说明
 ```
GFSClient(5)
read("a.txt")
>> null
write("a.txt", "World")
>> You don't need to return anything, but you need to call writeChunk("a.txt", 0, "World") to write a 5 bytes chunk to GFS.
read("a.txt")
>> "World"
write("b.txt", "111112222233")
>> You need to save "11111" at chunk 0, "22222" at chunk 1, "33" at chunk 2.
write("b.txt", "aaaaabbbbb")
read("b.txt")
>> "aaaaabbbbb"
```
 ### 参考代码
 ```java
/* Definition of BaseGFSClient
 * class BaseGFSClient {
 *     private Map<String, String> chunk_list;
 *     public BaseGFSClient() {}
 *     public String readChunk(String filename, int chunkIndex) {
 *         // Read a chunk from GFS
 *     }
 *     public void writeChunk(String filename, int chunkIndex,
 *                            String content) {
 *         // Write a chunk to GFS
 *     }
 * }
 */
public class GFSClient extends BaseGFSClient {

    public int chunkSize;
    public Map<String, Integer> chunkNum;

    public GFSClient(int chunkSize) {
        // initialize your data structure here
        this.chunkSize = chunkSize;
        this.chunkNum = new HashMap<String, Integer>();
    }
    
    // @param filename a file name
    // @return conetent of the file given from GFS
    public String read(String filename) {
        // Write your code here
        if (!chunkNum.containsKey(filename))
            return null;

        StringBuffer content = new StringBuffer();

        for (int i = 0; i < chunkNum.get(filename); ++i) {
            String sub_content = readChunk(filename, i);
            if (sub_content != null)
                content.append(sub_content);
        }
        return content.toString();
    }

    // @param filename a file name
    // @param content a string
    // @return void
    public void write(String filename, String content) {
        // Write your code here
        int length = content.length();

        int num = (length - 1) / chunkSize + 1;
        chunkNum.put(filename, num);

        for (int i = 0; i < num; ++i) {
            int start = i * chunkSize;
            int end = i == num -1 ? length : (i + 1) * chunkSize; 
            String sub_content = content.substring(start, end);
            writeChunk(filename, i, sub_content);
        }
    }
}

```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)