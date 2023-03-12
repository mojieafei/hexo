---
title: redis_string
date: 2023-03-09 22:32:15
tags: redis
comments: true
categories:
- redis
- 文档翻译
- 原创
---
### Redis Strings
Introduction to Redis strings
> 关于redis strings类型的介绍

Redis strings store sequences of bytes, including text, serialized objects, and binary arrays. As such, strings are the most basic Redis data type. They're often used for caching, but they support additional functionality that lets you implement counters and perform bitwise operations, too.
> string类型由多个bytes字节构成，包括文本、序列化对象、二进制的数组。因此，strings是最最基本的string存储数据类型，经常被用于缓存，但是strings也支持实现计数器及二进制位运算的操作额外的功能。

Examples
Store and then retrieve a string in Redis:
> 存储并检索字符串
<!--more-->
    SET user:1 salvatore
    OK
    GET user:1
    "salvatore"
Store a serialized JSON string and set it to expire 100 seconds from now:
> 存储一个序列化的JSON串并设置100秒之后过期

    SET ticket:27 "\"{'username': 'priya', 'ticket_id': 321}\"" EX 100
Increment a counter:
> 创建一个计数器

    INCR c
    (integer) 1
    INCRBY views:page:2 10
    (integer) 11
### Limits（存储大小极限）
By default, a single Redis string can be a maximum of 512 MB.
> 在默认的情况下，单个的redis string类型可以存储最大的大小为512兆。
### Basic commands
#### Getting and setting Strings
* SET stores a string value.
* SETNX stores a string value only if the key doesn't already exist. Useful for implementing locks.
* GET retrieves a string value.
* MGET retrieves multiple string values in a single operation.
>   获取和设置strings
> * SET 存储一个string值
> * SETNX 如果该值不存在则存储一个string值。对于锁操作非常有用。
> * GET 检索一个string值
> * MGET 一次操作里检索多个string值
### Managing counters
* INCRBY atomically increments (and decrements when passing a negative number) counters stored at a given key.
* Another command exists for floating point counters: INCRBYFLOAT.
>   管理编辑计数器
> * INCRBY 特定key的原子性递增（传递负值时候递减）
> * 浮点型数据的计数器请用其他命令：INCRBYFLOAT
### Bitwise operations
To perform bitwise operations on a string, see the bitmaps data type docs.
>   位运算操作
> 关于string的位运算操作，请查看[bitmaps数据类型]()文档

See the complete list of string commands.
> 请查看[string命令大全]()

### Performance
Most string operations are O(1), which means they're highly efficient. However, be careful with the SUBSTR, GETRANGE, and SETRANGE commands, which can be O(n). These random-access string commands may cause performance issues when dealing with large strings.
> 性能
> 大多数的string操作的复杂度都是O(1),意味着他们的是非常高速有效的。然而，需要小心使用SUBSTR、GETRANGE、SETRANGE命令，三者的复杂度是O(n)。处理大型字符串时，这些随机访问字符串命令可能会导致性能问题


### Alternatives
If you're storing structured data as a serialized string, you may also want to consider Redis hashes or RedisJSON.
> 其他方案
> 如果你存储结构化的数据并该序列化后的字符，你可以考虑一下redis的hashes类型或者RedisJSON类型。

### Learn more
Redis Strings Explained is a short, comprehensive video explainer on Redis strings.
Redis University's RU101 covers Redis strings in detail.
> 更多
> Redis 字符串解释是一个关于 Redis 字符串的简短、全面的视频解释器。
> [Redis University's RU101]()课程涵盖了redis strings的细节