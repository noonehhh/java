#Redis面试技术点整理

2019年3月14日21:40:28

## 数据结构
### String

大小限制：512MB
### 使用场景
1. 计数器 Incr/IncrBy/IncrByFloat/Decr/DecrBy（原子性）
2. 分布式锁
3. 限流
4. 分布式session
5. 用bitMap统计每天用户是否登录（每个用户占用一个offset位，默认为0 ，登录即设置为1）
```
setbit key offset value
getbit key offset
```
### List

#### 使用场景
1. 消息队列 lpush/rpop

### Hash

Hash成员比较少时，底层采用一维数组的方式存储，此时redisObject的encoding：zipmap。HashMap增大时自动转成hashMap，此时encoding：ht
### Set

最大值：2^32-1  内部实现为一个value永远为null的hash
#### 使用场景
1. 赞 踩 标签 好友关系

### Zset

#### 使用场景
1. 排行榜

### HyperLogLog

### Geo

## 使用场景





## 两种持久化方式

### RDB

基于快照，

### AOP

基于日志


## 分布式锁


问:如何使用redis实现分布式锁？

答:使用setnx获取锁。获取成功再用expire设置一个过期时间

问:如果setnx之后执行expire之前进程意外crash怎么办？

答:使用 jedis.set(key, value, "nx", "px, [过期时间]);(这才是正解)

```
- 获取锁（unique_value可以是UUID等）
SET resource_name unique_value NX PX 30000

- 释放锁（lua脚本中，一定要比较value，防止误解锁）
if redis.call("get",KEYS[1]) == ARGV[1] then
    return redis.call("del",KEYS[1])
else
    return 0
end
```


## 过期key清除原理

当Client主动访问key时，redis会先进行过期判断，如果已经过期就将其删除，除此之外，redis会在后台每100毫秒随机选择100个key判断是否过期（如果过期就删除掉），如果其中有超过25%key都过期了就会额外再选择100个key（不算在10次之内）进行相同的操作。
## 其他命令
### keys

### scan

## 内存饱和回收策略
1. volatile-lru: 从已设置过期时间的数据中选择最近最少使用的清楚
2. volatile-ttl: 从已设置过期时间的数据中选择将要过期的清楚
3. volatile-random: 从已设置过期时间的数据中随机选择清楚
4. allkeys-lru: 从所有数据集中清楚最近最少使用的
5. allkeys-random: 从所有数据中随机选择数据清楚
6. no-enviction：禁止驱逐数据


## redis.conf 部分说明
1. maxmemory:超过这个大小之后就拒绝写入数据。
2. vm-enabled:no //不要使用虚拟内存
3. hash-max-zipmap-entries 64 //当hash的value部分的Map内部不超过64个成员时候使用线性紧凑的zipmap存储，超过这个值自动转成ht存储
4. hash-max-zipmap-value 512 //hash的value的map内存每个成员值长度不超过512字节就会采用线性紧凑zipmap来存储 （以上3、4满足任意一个就会转换）

## 其他优化

Redis 缓存了一定范围的常量数字作为资源共享，在很多数据类型是数值型则能极大减少内存开销，默认为1-10000，可以重新编译配置修改源代码中的一行宏定义 REDIS_SHARED_INTEGERS。




## 参考资料
https://mp.weixin.qq.com/s/5eFUJtX-VP9HG35XXCLwjA
https://mp.weixin.qq.com/s?__biz=MzU5ODUwNzY1Nw==&mid=2247484155&idx=1&sn=0c73f45f2f641ba0bf4399f57170ac9b&scene=21#wechat_redirect
