# 账户合并
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/accounts-merge/?utm_source=sc-github-wzz)
 ## 题目描述
 给定一个帐户列表，每个元素`accounts [i]`是一个字符串列表，其中第一个元素`accounts [i] [0]`是账户名称，其余元素是这个帐户的电子邮件。
现在，我们想合并这些帐户。
如果两个帐户有相同的电子邮件地址，则这两个帐户肯定属于同一个人。
请注意，即使两个帐户具有相同的名称，它们也可能属于不同的人，因为两个不同的人可能会使用相同的名称。
一个人可以拥有任意数量的账户，但他的所有帐户肯定具有相同的名称。
合并帐户后，按以下格式返回帐户：每个帐户的第一个元素是名称，其余元素是**按字典序排序**后的电子邮件。
帐户本身可以按任何顺序返回。
 ### 样例说明
 ```
样例 1:
	输入:
	[
		["John", "johnsmith@mail.com", "john00@mail.com"],
		["John", "johnnybravo@mail.com"],
		["John", "johnsmith@mail.com", "john_newyork@mail.com"],
		["Mary", "mary@mail.com"]
	]
	
	输出: 
	[
		["John", 'john00@mail.com', 'john_newyork@mail.com', 'johnsmith@mail.com'],
		["John", "johnnybravo@mail.com"],
		["Mary", "mary@mail.com"]
	]

	解释: 
	第一个第三个John是同一个人的账户，因为这两个账户有相同的邮箱："johnsmith@mail.com".
	剩下的两个账户分别是不同的人。因为他们没有和别的账户有相同的邮箱。

	你可以以任意顺序返回结果。比如：
	
	[
		['Mary', 'mary@mail.com'],
		['John', 'johnnybravo@mail.com'],
		['John', 'john00@mail.com', 'john_newyork@mail.com', 'johnsmith@mail.com']
	]
	也是可以的。

```
 ### 参考代码
 使用算法强化版所讲的并查集。
```java
public class Solution {
    Map<Integer, Integer> father;
    /**
     * @param accounts: List[List[str]]
     * @return: return a List[List[str]]
     */
    public List<List<String>> accountsMerge(List<List<String>> accounts) {
        father = new HashMap();
        
        // union
        Map<String, List> emailToIds = getEmailToIds(accounts);
        for (String email : emailToIds.keySet()) {
            List<Integer> ids = emailToIds.get(email);
            for (int i = 1; i < ids.size(); i++) {
                union(ids.get(i), ids.get(0));
            }
        }
        
        // merge accounts
        Map<Integer, Set<String>> idToEmailSet = getIdToEmailSet(accounts);
        List<List<String>> mergedAccounts = new ArrayList<>();
        for (Integer id : idToEmailSet.keySet()) {
            List<String> sortedEmails = new ArrayList(idToEmailSet.get(id));
            Collections.sort(sortedEmails);
            sortedEmails.add(0, accounts.get(id).get(0));
            mergedAccounts.add(sortedEmails);
        }
        
        return mergedAccounts;
    }
    
    private Map<String, List> getEmailToIds(List<List<String>> accounts) {
        Map<String, List> emailToIds = new HashMap<>();
        for (int user_id  = 0; user_id < accounts.size(); user_id++) {
            List<String> account = accounts.get(user_id);
            for (int i = 1; i < account.size(); i++) {
                List<Integer> ids = emailToIds.getOrDefault(account.get(i), new ArrayList<Integer>());
                ids.add(user_id);
                emailToIds.put(account.get(i), ids);
            }
        }
        return emailToIds;
    }
    
    private Map<Integer, Set<String>> getIdToEmailSet(List<List<String>> accounts) {
        Map<Integer, Set<String>> idToEmailSet = new HashMap<>();
        for (int user_id  = 0; user_id < accounts.size(); user_id++) {
            int root_id = find(user_id);
            Set<String> emailSet = idToEmailSet.getOrDefault(root_id, new HashSet<String>());
            List<String> account = accounts.get(user_id);
            for (int i = 1; i < account.size(); i++) {
                emailSet.add(account.get(i));
            }
            idToEmailSet.put(root_id, emailSet);
        }
        return idToEmailSet;
    }
    
    private int find(int id) {
        List<Integer> path = new ArrayList<>();
        while (father.containsKey(id)) {
            path.add(id);
            id = father.get(id);
        }
        
        for (Integer i : path) {
            father.put(i, id);
        }
        
        return id;
    }
    
    private void union(int id1, int id2) {
        int root1 = find(id1);
        int root2 = find(id2);
        if (root1 != root2) {
            father.put(root1, root2);
        }
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)