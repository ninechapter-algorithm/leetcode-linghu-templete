# 有序链表转换为二叉搜索树
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/convert-sorted-list-to-binary-search-tree/?utm_source=sc-github-wzz)
 ## 题目描述
 <p>给出一个所有元素以升序排序的单链表，将它转换成一棵高度平衡的二叉搜索树</p>
 ### 样例说明
 ```
样例 1:
	输入: array = 1->2->3
	输出:
		 2  
		/ \
		1  3
		
样例 2:
	输入: 2->3->6->7
	输出:
		 3
		/ \
	       2   6
		     \
		      7

	解释:
	可能会有多个符合要求的结果，返回任意一个即可。
```
 ### 参考代码
 Given a singly linked list where elements are sorted in ascending order, convert it to a height balanced BST.

高度平衡，所以将链表从中间分开，左边是左子树，右边是右子树。
```cpp
// version 1: (Recommend)
class Solution {
public:
    /**
     * @param head: The first node of linked list.
     * @return: a tree node
     */
    TreeNode *sortedListToBST(ListNode *head) {
        if (head == NULL) {
            return NULL;
        }
        int size = getListSize(head);
        return convertHelper(head, size);
    }
    
    int getListSize(ListNode *head) {
        int size = 0;
        while (head != NULL) {
            head = head->next;
            size++;
        }
        return size;
    }
    
    TreeNode *convertHelper(ListNode *&head, int size) {
        if (size == 0) {
            return NULL;
        }
        
        TreeNode *root = new TreeNode(0);
        root->left = convertHelper(head, size / 2);
        root->val = head->val; head = head->next;
        root->right = convertHelper(head, size - size / 2 - 1);
        return root;
    }
};

// version 2:
struct ResultType {
    TreeNode *tree;
    ListNode *next;
};

class Solution {
public:
    /**
     * @param head: The first node of linked list.
     * @return: a tree node
     */
    TreeNode *sortedListToBST(ListNode *head) {
        if (head == NULL) {
            return NULL;
        }
        
        int size = getListSize(head);
        ResultType result = convertHelper(head, size);
        return result.tree;
    }
    
    int getListSize(ListNode *head) {
        int size = 0;
        while (head != NULL) {
            head = head->next;
            size++;
        }
        return size;
    }
    
    ResultType convertHelper(ListNode *head, int size) {
        ResultType result;
        
        if (size == 1) {
            result.tree = new TreeNode(head->val);
            result.next = head->next;
            return result;
        }
        
        ResultType left = convertHelper(head, size / 2);
        result.tree = new TreeNode(left.next->val);
        result.tree->left = left.tree;
        if (left.next->next == NULL || size - size / 2 - 1 == 0) {
            result.tree->right = NULL;
            result.next = left.next->next;
            return result;
        }
        ResultType right = convertHelper(left.next->next, size - size / 2 - 1);
        result.tree->right = right.tree;
        result.next = right.next;
        return result;
    }
};
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)