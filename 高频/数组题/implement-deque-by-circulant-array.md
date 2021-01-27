# 用循环数组实现双向队列
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/implement-deque-by-circulant-array/?utm_source=sc-github-wzz)
 ## 题目描述
 用循环数组来实现双端队列。你需要支持下列方法：
CircularDeque(n): 初始化一个大小为n的循环数组来存储元素
boolean isFull(): 如果数组满了就返回 true
boolean isEmpty(): 如果数组为空则返回 true
void pushFront(element): 往队列的头部添加一个元素
int popFront(): 从队列的头部弹出一个元素
void pushBack(element): 往队列的尾部添加一个元素
int popBack(): 从队列的尾部弹出一个元素
 ### 样例说明
 
 ### 参考代码
 ### 数据结构设计
#### 算法思路
设计一个管理下标的函数，将任意下标转化为合法下标$(0 \leq i \le n)$
用$front$ $rear$ $size$分别记录数组的头、尾、大小
对于构造函数$CircularDeque$，需要初始化数组和$front$ $rear$ $size$，因为一开始数组大小为$0$，所以$front$需要比$rear$后一个位置
对于$isEmpty$ $isFull$两个方法，可以对$size$进行判断
对于四个涉及数组操作的方法，先找到需要处理的位置，处理完毕之后再修改数组的$front$ $rear$ $size$信息

#### 复杂度分析
- 时间复杂度为 $O(n)$
    - n为数组的大小，因为初始化数组需要开辟大小为n的空间，除了构造函数$CircularDeque$外的函数时间复杂度均为 $O(1)$
- 空间复杂度为 $O(n)$
    - n为数组的大小，因为初始化数组需要开辟大小为n的空间

```
[[java]]
public class CircularDeque {    
    int[] circularArray;
    int front;
    int rear;
    int size;
    
    public CircularDeque(int n) {
        this.circularArray = new int[n];
        front = getCircularIndex(1);
        rear = getCircularIndex(0);
        size = 0;
    }
    
    private int getCircularIndex(int p) {
        int len = circularArray.length;
        return (p % len + len) % len;
    }
    
    public boolean isFull() {
        return size == circularArray.length;
    }

    public boolean isEmpty() {
        return size == 0;
    }

    public void pushFront(int element) {
        int index = getCircularIndex(front - 1);
        circularArray[index] = element;
        front = index;
        size++;
    }
     
    public void pushBack(int element) {
        int index = getCircularIndex(rear + 1);
        circularArray[index] = element;
        rear = index;
        size++;
    }

    public int popFront() {
        int index = front;
        int ele = circularArray[index];
        front = getCircularIndex(index + 1);
        size--;
        return ele;
    }
    
    public int popBack() {
        int index = rear;
        int ele = circularArray[index];
        rear = getCircularIndex(index - 1);
        size--;
        return ele;
    }
}

[[cpp]]
class CircularDeque {
public:
    vector<int> circularArray;
    int front;
    int rear;
    int size;
    
    CircularDeque(int n) {
        circularArray.resize(n, 0);
        front = getCircularIndex(1);
        rear = getCircularIndex(0);
        size = 0;
    }
    
    bool isFull() {
        return size == circularArray.size();
    }

    bool isEmpty() {
        return size == 0;
    }

    void pushFront(int element) {
        int index = getCircularIndex(front - 1);
        circularArray[index] = element;
        front = index;
        size++;
    }

    int popFront() {
        int index = front;
        int ele = circularArray[index];
        front = getCircularIndex(index + 1);
        size--;
        return ele;
    }

    void pushBack(int element) {
        int index = getCircularIndex(rear + 1);
        circularArray[index] = element;
        rear = index;
        size++;
    }

    int popBack() {
        int index = rear;
        int ele = circularArray[index];
        rear = getCircularIndex(index - 1);
        size--;
        return ele;
    }
    
private:
    int getCircularIndex(int p) {
        int len = circularArray.size();
        return (p % len + len) % len;
    }
};

[[python]]
class CircularDeque:
    def __init__(self, n):
        self.circularArray = [0] * n
        self.front, self.rear = 1, 0
        self.size = 0
    
    def getCircularIndex(self, p):
        length = len(self.circularArray)
        return (p % length + length) % length
    
    def isFull(self):
        return self.size == len(self.circularArray)

    def isEmpty(self):
        return self.size == 0

    def pushFront(self, element):
        index = self.getCircularIndex(self.front - 1);
        self.circularArray[index] = element;
        self.front = index;
        self.size += 1;
        
    def popFront(self):
        index = self.front;
        ele = self.circularArray[index];
        self.front = self.getCircularIndex(index + 1);
        self.size -= 1;
        return ele;
        
    def pushBack(self, element):
        index = self.getCircularIndex(self.rear + 1);
        self.circularArray[index] = element;
        self.rear = index;
        self.size += 1;

    def popBack(self):
        index = self.rear;
        ele = self.circularArray[index];
        self.rear = self.getCircularIndex(index - 1);
        self.size -= 1;
        return ele;

```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)