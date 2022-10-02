# Redis
--------

### 类型

+ [string](#string)
+ [hash](#hash)
+ [list](#list)
+ [set](#set)
+ [zset](#zset) (sorted set：有序集合)

#### string


#### hash
Redis hash 是一个 string 类型的 field（字段） 和 value（值） 的映射表，hash 特别适合用于存储对象。

Redis 中每个 hash 可以存储 232 - 1 键值对（40多亿）。

**[key] : [field] [value]**

`hmset person name "huahua" age 11`

[opt link](https://www.runoob.com/redis/redis-hashes.html) 

#### list
#### set
#### zset

### OPT

查看所有Key
`keys *` 

查看安装目录
`config get dir` 

备份

`save` 

+ 同步阻塞的 会在安装目录下创建备份文件 **dump.rdb** 

`bgsave` 

+ 异步的
