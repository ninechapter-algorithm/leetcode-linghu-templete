# 添加运算符
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/add-operators/?utm_source=sc-github-wzz)
 ## 题目描述
 给定一个仅包含数字 `0` - `9` 的字符串和一个目标值，返回在数字之间添加了 **二元** 运算符(不是一元)`+`, `-` 或 `*` 之后所有能得到目标值的情况。
 ### 样例说明
 
 ### 参考代码
 ```java
public class Solution {
    /**
     * @param num a string contains only digits 0-9
     * @param target an integer
     * @return return all possibilities
     */
    public List<String> addOperators(String num, int target) {
        // Write your code here
        List<String> results = new ArrayList<String>();
        if (num == null || num.length() == 0) {
            return results;
        }
        helper(results, "", num, target, 0, 0, 0);
        return results;
    }
    public void helper(List<String> results, String path, String num, int target, int pos, long eval, long multed){
        if (pos == num.length()){
            if(target == eval)
                results.add(path);
            return;
        }
        for (int i = pos; i < num.length(); i++) {
            if (i != pos && num.charAt(pos) == '0') {
                break;
            }
            long cur = Long.parseLong(num.substring(pos, i + 1));
            if (pos == 0) {
                helper(results, path + cur, num, target, i + 1, cur, cur);
            } else {
                helper(results, path + "+" + cur, num, target, i + 1, eval + cur , cur);
                helper(results, path + "-" + cur, num, target, i + 1, eval -cur, -cur);
                helper(results, path + "*" + cur, num, target, i + 1, eval - multed + multed * cur, multed * cur );
            }
        }
    }
}


// version: 高频题班
public class Solution {
    /**
     * @param num    a string contains only digits 0-9
     * @param target an integer
     * @return return all possibilities
     */

    void dfs(String num, int target, int start, String str, long sum, long lastF, List<String> ans) {
        if (start == num.length()) {
            if (sum == target) {
                ans.add(str);
            }
            return;
        }
        for (int i = start; i < num.length(); i++) {
            long x = Long.parseLong(num.substring(start, i + 1));

            if (start == 0) {
                dfs(num, target, i + 1, "" + x, x, x, ans);
            } else {
                dfs(num, target, i + 1, str + "*" + x, sum - lastF + lastF * x, lastF * x, ans);
                dfs(num, target, i + 1, str + "+" + x, sum + x, x, ans);
                dfs(num, target, i + 1, str + "-" + x, sum - x, -x, ans);
            }
            if (x == 0) {
                break;
            }
        }
    }

    public List<String> addOperators(String num, int target) {
        // Write your code here
        List<String> ans = new ArrayList<>();
        dfs(num, target, 0, "", 0, 0, ans);
        return ans;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)