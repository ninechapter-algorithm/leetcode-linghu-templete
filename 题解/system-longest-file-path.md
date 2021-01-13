# 最长绝对文件路径
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/system-longest-file-path/?utm_source=sc-github-wzz)
 ## 题目描述
 假设我们通过以下的方式用字符串来抽象我们的文件系统：
字符串`"dir\n\tsubdir1\n\tsubdir2\n\t\tfile.ext"`代表了：
```
dir
	subdir1
	subdir2
		file.ext
```
目录 `dir` 包含一个空子目录 `subdir1` 和一个包含文件file.ext的子目录 `subdir2`。
字符串
```
"dir\n\tsubdir1\n\t\tfile1.ext\n\t\tsubsubdir1\n\tsubdir2\n\t\tsubsubdir2\n\t\t\tfile2.ext"
```
代表了：
```
dir
	subdir1
		file1.ext
		subsubdir1
	subdir2
		subsubdir2
			file2.ext
```
目录 `dir` 包含两个子目录 `subdir1` 和 `subdir2` 。 `subdir1` 包含一个文件 file1.ext 和一个空的二级子目录 `subsubdir1` 。 `subdir2` 包含一个包含文件 file2.ext 的二级子目录 `subsubdir2`。 
我们有兴趣找到文件系统中文件的最长绝对路径（字符数）。例如，在上面的第二个例子中，最长的绝对路径是`“dir/subdir2/subsubdir2/file2.ext”`，其长度为 `32` (不包括双引号)。
给定一个以上述格式表示文件系统的字符串，返回抽象文件系统中文件最长绝对路径的长度。如果系统中没有文件，则返回 `0` 。
 ### 样例说明
 
 ### 参考代码
 ```java
public class Solution {
    /**
     * @param input an abstract file system
     * @return return the length of the longest absolute path to file
     */
    public int lengthLongestPath(String input) {
        // Write your code here
        int result = 0;
        int[] path = new int[input.length() + 2];
        String[] st = input.split("\n");
        for (String line : st){
            String name = line.replaceAll("(\t)+", "");
            int depth = line.length() - name.length();
            if(name.contains("."))
                result = Math.max(result, path[depth] + name.length());
            else
                path[depth + 1] = path[depth] + name.length() + 1;
        }
        return result;
    }
}

// version: 高频题班
public class Solution {
    /*
     * @param input an abstract file system
     * @return return the length of the longest absolute path to file
     */
    public int lengthLongestPath(String input) {
        // Write your code here
        if (input.length() == 0) {
            return 0;
        }
        int ans = 0;
        int[] sum = new int[input.length() + 1];

        for (String line : input.split("\n")) {
            int level = line.lastIndexOf('\t') + 2;
            int len = line.length() - (level - 1);
            if (line.contains(".")) {
                ans = Math.max(ans, sum[level - 1] + len);
            } else {
                sum[level] = sum[level - 1] + len + 1;
            }
        }
        return ans;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)