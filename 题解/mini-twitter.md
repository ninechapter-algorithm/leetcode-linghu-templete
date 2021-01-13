# 迷你推特
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/mini-twitter/?utm_source=sc-github-wzz)
 ## 题目描述
 实现一个迷你的推特，支持下列几种方法

1. `postTweet(user_id, tweet_text).` 发布一条推特.
2. `getTimeline(user_id).` 获得给定用户最新发布的十条推特，按照发布时间从最近的到之前排序
3. `getNewsFeed(user_id).` 获得给定用户的朋友或者他自己发布的最新十条推特，从发布时间最近到之前排序
4. `follow(from_user_id, to_user_id).` from_user_id 关注 to_user_id.
5. `unfollow(from_user_id, to_user_id).` from_user_id 取消关注 to_user_id.
 ### 样例说明
 
 ### 参考代码
 因为题目里涉及到对推文按照时间排序, 同时 Tweet 类本身不含时间信息, 所以我们需要额外地记录每条推文发出的时间.

可以定义一个类的静态变量作为计数器来实现.

然后分析我们需要的数据结构:

- `class Node {Tweet, int};` 对原有的Tweet类的扩展, 使其可以记录时间 (当然, 也可以用类的继承来实现)
- `map<int, vector<Node>>` 用户id到这个用户发送了的推文的映射
- `map<int, set<int>>` 用户id到这个用户关注的人的id的映射

然后对应每种方法的实现:

- `postTweet()` 直接添加到`map<int, vector<Node>>`中即可
- `getTimeline()` 根据`map<int, vector<Node>>`获得该用户的最新推文, 返回即可
- `getNewsFeed()` 同时用到上面定义的两个映射, 比较暴力的做法是获取这些用户的所有推文, 排序, 拿出前十个; 或者可以利用堆进行 "多路归并"
- `follow()` 在 `map<int, set<int>>` 中添加即可
- `unfollow()` 在 `map<int, set<int>>` 中删除即可

(本题解使用C++相关数据结构描述, 不过映射和集合在其他语言中也有对应的实现)
```java
/**
 * Definition of Tweet:
 * public class Tweet {
 *     public int id;
 *     public int user_id;
 *     public String text;
 *     public static Tweet create(int user_id, String tweet_text) {
 *         // This will create a new tweet object,
 *         // and auto fill id
 *     }
 * }
 */
public class MiniTwitter {
    class Node {
        public int order;
        public Tweet tweet;

        public Node(int o, Tweet t) {
            this.order = o;
            this.tweet = t;
        }
    }

    class SortByOrder implements Comparator {
        public int compare(Object obj1, Object obj2) {
            Node node1 = (Node) obj1;
            Node node2 = (Node) obj2;
            if (node1.order < node2.order)
                return 1;
            else
                return -1;
        }
    }

    private Map<Integer, Set<Integer>> friends;
    private Map<Integer, List<Node>> users_tweets;
    private int order;

    public List<Node> getLastTen(List<Node> tmp) {
        int last = 10;
        if (tmp.size() < 10)
            last = tmp.size();
        return tmp.subList(tmp.size() - last, tmp.size());
    }

    public List<Node> getFirstTen(List<Node> tmp) {
        int last = 10;
        if (tmp.size() < 10)
            last = tmp.size();
        return tmp.subList(0, last);
    }

    public MiniTwitter() {
        // initialize your data structure here.
        this.friends = new HashMap<Integer, Set<Integer>>();
        this.users_tweets = new HashMap<Integer, List<Node>>();
        this.order = 0;
    }

    // @param user_id an integer
    // @param tweet a string
    // return a tweet
    public Tweet postTweet(int user_id, String tweet_text) {
        // Write your code here
        Tweet tweet = Tweet.create(user_id, tweet_text);
        if (!users_tweets.containsKey(user_id))
            users_tweets.put(user_id, new ArrayList<Node>());
        order += 1;
        users_tweets.get(user_id).add(new Node(order, tweet));
        return tweet;
    }

    // @param user_id an integer
    // return a list of 10 new feeds recently
    // and sort by timeline
    public List<Tweet> getNewsFeed(int user_id) {
        // Write your code here
        List<Node> tmp = new ArrayList<Node>();
        if (users_tweets.containsKey(user_id))
            tmp.addAll(getLastTen(users_tweets.get(user_id)));

        if (friends.containsKey(user_id)) {
            for (Integer user : friends.get(user_id)) {
                if (users_tweets.containsKey(user))
                    tmp.addAll(getLastTen(users_tweets.get(user)));
            }
        }

        Collections.sort(tmp, new SortByOrder());
        List<Tweet> rt = new ArrayList<Tweet>();
        tmp = getFirstTen(tmp);
        for (Node node : tmp) {
            rt.add(node.tweet);
        }
        return rt;
    }

    // @param user_id an integer
    // return a list of 10 new posts recently
    // and sort by timeline
    public List<Tweet> getTimeline(int user_id) {
        // Write your code here
        List<Node> tmp = new ArrayList<Node>();
        if (users_tweets.containsKey(user_id))
            tmp.addAll(getLastTen(users_tweets.get(user_id)));

        Collections.sort(tmp, new SortByOrder());
        List<Tweet> rt = new ArrayList<Tweet>();
        tmp = getFirstTen(tmp);
        for (Node node : tmp)
            rt.add(node.tweet);
        return rt;
    }

    // @param from_user_id an integer
    // @param to_user_id an integer
    // from user_id follows to_user_id
    public void follow(int from_user_id, int to_user_id) {
        // Write your code here
        if (!friends.containsKey(from_user_id))
            friends.put(from_user_id, new HashSet<Integer>());

        friends.get(from_user_id).add(to_user_id);
    }

    // @param from_user_id an integer
    // @param to_user_id an integer
    // from user_id unfollows to_user_id
    public void unfollow(int from_user_id, int to_user_id) {
        // Write your code here
        if (friends.containsKey(from_user_id))
            friends.get(from_user_id).remove(to_user_id);
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)