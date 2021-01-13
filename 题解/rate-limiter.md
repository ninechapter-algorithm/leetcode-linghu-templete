# 限制器
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/rate-limiter/?utm_source=sc-github-wzz)
 ## 题目描述
 1367
 ### 样例说明
 1367
 ### 参考代码
 ```java
public class RateLimiter {
    private HashMap<String, List<Integer>> map = new HashMap<>();
    
    /**
     * @param timestamp the current timestamp
     * @param event the string to distinct different event
     * @param rate the format is [integer]/[s/m/h/d]
     * @param increment whether we should increase the counter
     * @return true of false to indicate the event is limited or not
     */
    public boolean isRatelimited(int current_timestamp, String event, String rate, boolean increment) {
        // Write your code here
        int start = rate.indexOf("/");
        int limit = Integer.parseInt(rate.substring(0, start));
        String type = rate.substring(start + 1, rate.length());

        int duration = 1;
        if (type.equals("m"))
            duration = duration * 60;
        else if (type.equals("h"))
            duration = duration * 60 * 60;
        else if (type.equals("d"))
            duration = duration * 60 * 60 * 24;
        int start_timestamp = current_timestamp - duration + 1;
        
        if (!map.containsKey(event))
            map.put(event, new ArrayList<Integer>());

        int count = count_events(map.get(event), start_timestamp);
        boolean is_ratelimited = count >= limit;
        if (increment && !is_ratelimited)
            insert_event(map.get(event), current_timestamp);
        return is_ratelimited;
    }

    public void insert_event(List<Integer> event, int timestamp) {
        event.add(timestamp);
    }

    // use binary search algorithm to count how many events happened
    // after start_timestamp because event is sorted by timestamp
    public int count_events(List<Integer> event, int start_timestamp) {
        int l = 0, r = event.size() - 1;
        if (r == -1)
            return 0;
        if (event.get(r) < start_timestamp) 
            return 0;
        int ans = 0;
        while (l <= r) {
            int mid = (l + r) >> 1;
            if (event.get(mid) >= start_timestamp) {
                ans = mid;
                r = mid - 1;
            } else
                l = mid + 1;
        }
        return event.size() - 1 - ans + 1;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)