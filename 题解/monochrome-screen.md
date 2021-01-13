# 黑白屏
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/monochrome-screen/?utm_source=sc-github-wzz)
 ## 题目描述
 一个黑白显示屏由一个单独的字节数组组成，这个屏幕允许 8 个连续像素由一个字节进行存储。该显示屏宽 w ，被分割为 8 （也就是说，任意字节都不可能被行切断）。该显示屏高，则取决于数组的长度及显示屏的宽。请设计一个函数 `drawHorizontalLine(byte[] screen, int width, int x1, int x2, int y)` 从(x1, y) 到 (x2, y) 画出一条水平线。
 ### 样例说明
 **样例1**
```plain
输入:
初始屏幕 = [0]
屏宽 = 8
x1 = 0
x2 = 7 
y = 0
输出: [255]
样例解释:
[0] 意味着一开始屏幕的二进制表示是 00000000。你需要把他转换为 [255](11111111)
```

**样例2**
```plain
输入:
初始屏幕 = [0,0,0,0]
屏宽 = 16
x1 = 5
x2 = 11 
y = 1
输出: [0,0,7,240]
样例解释:
[0,0,0,0] 意味着初始屏幕的第一行是 00000000,00000000 ，第二行是 00000000,00000000。你需要把他转换为[0,0,7,240](00000000,00000000,00000111,11110000)
```
 ### 参考代码
 此题按照题目要求，找到起始点和终点在屏幕表示里的位置，然后再对应的二进制里面进行修改即可。
```java
public class Solution {
    /**
     * @param screen an array of 8bit integer(byte)
     * @param width the width of screen
     * @param x1 an integer
     * @param x2 an integer
     * @param y an integer
     * @return nothing
     */
    public void drawHorizontalLine(byte[] screen, int width, int x1, int x2, int y) {
        // Write your code here
        //找到起始点和终点的对应区域范围
        int start_offset = x1 % 8;
        int first_full_byte = x1 / 8;
        if (start_offset != 0) {
            first_full_byte++;
        }
        
        int end_offset = x2 % 8;
        int last_full_byte = x2 / 8;
        if (end_offset != 7) {
            last_full_byte--;
        }

        // Set full bytes
        for (int b = first_full_byte; b <= last_full_byte; b++) {
            screen[(width / 8) * y + b] = (byte) 0xFF;
        }

        // Create masks for start and end of line
        byte start_mask = (byte) (0xFF >> start_offset);
        byte end_mask = (byte) ~(0xFF >> (end_offset +1));
        // Set start and end of line
        if ((x1 / 8) == (x2 / 8)) { // x1 and x2 are in the same byte
            byte mask = (byte) (start_mask & end_mask);
            screen[(width / 8) * y + (x1 / 8)] |= mask;
        } else {
            if (start_offset != 0) {
                int byte_number = (width / 8) * y + first_full_byte - 1;
                screen[byte_number] |= start_mask;
            }

            if (end_offset != 7) {
                int byte_number = (width / 8) * y + last_full_byte + 1;
                screen[byte_number] |= end_mask;
            }
        }
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)