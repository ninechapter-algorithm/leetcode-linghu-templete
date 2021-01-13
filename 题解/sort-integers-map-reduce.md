# 排序(Map Reduce)
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/sort-integers-map-reduce/?utm_source=sc-github-wzz)
 ## 题目描述
 通过Map Reduce框架对整数进行排序
在mapper中， key为可以忽略的文档id， value是待排序的整数.
在reducer中, 你可以指定什么是key或者value(取决于你是如何实现你的mapper类的).对于输出的reducer类, key可以是任意， 但value需要有序(顺序取决于你什么时候输出) 
 ### 样例说明
 例1:
```
输入:
1: [14,7,9]
2: [10,1]
3: [2,5,6,3]
4: []
输出:
[1,2,3,5,6,7,9,10,14]

```

例2:
```
输入:
1: [14,7]
输出:
[7,14]

```


 ### 参考代码
 在reduce里，对相应的Integer利用PriorityQueue排序即可
```cpp
/**
 * Definition of Input:
 * template<class T>
 * class Input {
 * public:
 *     bool done(); 
 *         // Returns true if the iteration has elements or false.
 *     void next();
 *         // Move to the next element in the iteration
 *         // Runtime error if the iteration has no more elements
 *     T value();
 *        // Get the current element, Runtime error if
 *        // the iteration has no more elements
 * }
 */
class SortIntegersMapper: public Mapper {
public:
    void Map(int _, Input<vector<int>>* input) {
        // Write your code here
        // Please directly use func 'output' to output 
        // the results into output buffer.
        // void output(string &key, vector<int>& value);
        while (!input->done()) {
            vector<int> value = input->value();
            sort(value.begin(), value.end());
            string temp = "ignore_key";
            output(temp, value);
            input->next();
        }
    }
};

class Node {
public:
    int row, col, val;
    Node(int _r, int _c, int _v): row(_r), col(_c), val(_v){};
    bool operator < (const Node& obj) const {
        return val > obj.val;
    }
};

class SortIntegersReducer: public Reducer {
public:
    void Reduce(string &key, vector<vector<int>>& input) {
        // Write your code here
        // Please directly use func 'output' to output 
        // the results into output buffer.
        // void output(string &key, vector<int>& value);
        vector<int> results;
        if (input.size() == 0) {
            output(key, results);
            return;
        }

        int k = input.size();
        priority_queue<Node> queue;

        for (int i = 0; i < k; ++i) {
            if (input[i].size() > 0)
                queue.push(Node(i, 0, input[i][0]));
        }

        while (!queue.empty()) {
            Node temp = queue.top();
            queue.pop();
            int row = temp.row;
            int col = temp.col;
            int val = temp.val;
            results.push_back(val);
            if (col + 1 < input[row].size())
                queue.push(Node(row, col + 1, input[row][col + 1]));
        }

        output(key, results);
    }
};
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)