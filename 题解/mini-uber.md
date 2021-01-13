# 迷你优步
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/mini-uber/?utm_source=sc-github-wzz)
 ## 题目描述
 实现一个迷你优步
1. 司机提供他们的位置
2. 用户请求，然后返回一个匹配的司机

实现下列函数

- `report(driver_id, lat, lng)`
  - 如果没有找到匹配的trip，返回null
  - 否则返回匹配trip信息
- `request(rider_id, lat, lng)`
  1. 建立一个trip
  2. 找到一个最近的司机，标记这个司机为不可用
  3. 将司机id填入trip
  4. 返回trip

Java中trip的定义
```
public class Trip {
    public int id; // trip's id, primary key
    public int driver_id, rider_id; // foreign key
    public double lat, lng; // pick up location
}
```
 ### 样例说明
 **样例 1:**

```
输入:
  report(1, 36.1344, 77.5672) 
  report(2, 45.1344, 76.5672) 
  request(2, 39.1344, 76.5672) 
  report(1, 38.1344, 75.5672) 
  report(2, 45.1344, 76.5672) 
输出: 
  null
  null
  LOG(INFO): Trip(rider_id: 2, driver_id: 1, lat: 39.1344, lng: 76.5672)
  LOG(INFO): Trip(rider_id: 2, driver_id: 1, lat: 39.1344, lng: 76.5672)
  null
```

**样例 2:**

```
输入: 
  report(1, 36.1344, 77.5672)
  report(2, 45.1344, 76.5672)
  request(2, 39.1344, 76.5672)
  request(3, 78.1344, 134.5672)
输出: 
  null
  null
  LOG(INFO): Trip(rider_id: 2, driver_id: 1, lat: 39.1344, lng: 76.5672)
  LOG(INFO): Trip(rider_id: 3, driver_id: 2, lat: 78.1344, lng: 134.5672)
```
 ### 参考代码
 需要使用两个映射, 分别是 司机id -> 司机位置, 司机id -> trip.

大多语言都提供了这样的数据结构, Java HashMap, C++ map, python dict.

- `report(dirver_id, lat, lng)`
  1. 如果在 dirver_id -> trip 的映射中查找到对应的trip, 直接返回
  2. 没有查找到trip, 更新 dirver_id -> location 中的位置信息
- `request(rider_id, lat, lng)`
  1. 遍历 driver_id -> location , 选择距离最近的司机
  2. 建立 trip 并添加至 driver_id -> trip
  3. 将该司机从 dirver_id -> location 中删除
  
即司机id->司机位置这个映射中保存的是可用的司机.
```java
/**
 * Definition of Trip:
 * public class Trip {
 *     public int id; // trip's id, primary key
 *     public int driver_id, rider_id; // foreign key
 *     public double lat, lng; // pick up location
 *     public Trip(int rider_id, double lat, double lng);
 * }
 * Definition of Helper
 * class Helper {
 *     public static double get_distance(double lat1, double lng1,
                                         double lat2, double lng2) {
 *         // return distance between (lat1, lng1) and (lat2, lng2)
 *     }
 * };
 */
class Location {
    public double lat, lng;
    public Location(double _lat, double _lng) {
        lat = _lat;
        lng = _lng;
    }
}

public class MiniUber {

    Map<Integer, Trip> driver2Trip = null;
    Map<Integer, Location> driver2Location = null;

    public MiniUber() {
        // initialize your data structure here.
        driver2Trip = new HashMap<Integer, Trip>();
        driver2Location = new HashMap<Integer, Location>();
    }

    // @param driver_id an integer
    // @param lat, lng driver's location
    // return matched trip information if there have matched rider or null
    public Trip report(int driver_id, double lat, double lng) {
        // Write your code here
        if (driver2Trip.containsKey(driver_id))
            return driver2Trip.get(driver_id);

        if (driver2Location.containsKey(driver_id)) {
            driver2Location.get(driver_id).lat = lat;
            driver2Location.get(driver_id).lng = lng;
        } else {
            driver2Location.put(driver_id, new Location(lat, lng));
        }
        return null;
    }

    // @param rider_id an integer
    // @param lat, lng driver's location
    // return a trip
    public Trip request(int rider_id, double lat, double lng) {
        // Write your code here
        Trip trip = new Trip(rider_id, lat, lng);
        double distance = -1;
        int driver_id = -1;
        for (Map.Entry<Integer, Location> entry : driver2Location.entrySet()) {
            Location location = entry.getValue();
            double dis = Helper.get_distance(location.lat, location.lng, lat, lng);
            if (distance < 0 || distance > dis) {
                driver_id = entry.getKey();
                distance = dis;
            }
        }

        if (driver_id != -1)
            driver2Location.remove(driver_id);
        trip.driver_id = driver_id;
        driver2Trip.put(driver_id, trip);
        return trip;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)