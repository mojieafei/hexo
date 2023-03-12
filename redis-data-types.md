---
title: redis-data-types
date: 2023-03-07 14:16:31
tags: redis
comments: true
categories:
- redis
- 文档翻译
- 原创
---

# Redis data types

redis的数据类型

## Overview of data types supported by Redis

redis支持的数据类型概述

Redis is a data structure server. At its core, Redis provides a collection of native data types that help you solve a wide variety of problems, from caching to queuing to event processing. Below is a short description of each data type, with links to broader overviews and command references.

> redis是数据库服务器，其核心就是采用原生数据帮助你解决小到缓存，大到队列的各种各样的问题。下面是对数据类型的简要描述，以及命令参考的链接

If you'd like to try a comprehensive tutorial, see the Redis data types tutorial.

> 如果你想要更全面的指导，详情请查看
> [Redis data types tutorial]()
<!--more-->

### Core

#### Strings

Redis strings are the most basic Redis data type, representing a sequence of bytes. For more information, see:

Overview of Redis strings
Redis string command reference

> redis中strings是用的最多的最基本的数据类型，用byte字节作为存储单位，想看更多，请查看：
> 
> [redis strings类型介绍](http://daveafei2.softether.net:4000/2023/03/09/redis-string/)
> 
> [redis string命令大全](http://daveafei2.softether.net:4000/2023/03/09/redis-string-command/)

#### Lists

Redis lists are lists of strings sorted by insertion order. For more information, see:

Overview of Redis lists
Redis list command reference

> redis中lists是有序的string集合，想看更多，请查看：
> 
> [redis list类型介绍]()
> 
> [list 命令大全]()

#### Sets

Redis sets are unordered collections of unique strings that act like the sets from your favorite programming language (for example, Java HashSets, Python sets, and so on). With a Redis set, you can add, remove, and test for existence O(1) time (in other words, regardless of the number of set elements). For more information, see:

Overview of Redis sets
Redis set command reference

> redis 中sets类型像你最喜爱的开发语言一样，是一种无序且唯一的string集合（举个栗子，java里面的hashsets类型，python里面的sets类型等等）。
> 
> redis中的set类型，你可以添加，删除，检验是否存在，都只需要O(1)的时间复杂度（换句话说，不用在意集合里面有多少成员）。想看更多，请查看：
> 
> [redis sets类型介绍]()
> 
> [set命令大全]()



#### Hashes

Redis hashes are record types modeled as collections of field-value pairs. As such, Redis hashes resemble Python dictionaries, Java HashMaps, and Ruby hashes. For more information, see:

Overview of Redis hashes
Redis hashes command reference

> redis中hash是以k-v结构的集合类型。这一点，就像是python的dictionaries，java的HashMaps，以及ruby中的hashes。想看更多，请查看：
> 
> [redis hash类型介绍]()
> 
> [hash命令大全]()

#### Sorted sets

Redis sorted sets are collections of unique strings that maintain order by each string's associated score. For more information, see:

Overview of Redis sorted sets
Redis sorted set command reference

> redis中的唯一且有序集合，排序由对应的分值进行排序。想看更多，请查看：
> 
> [redis zset类型介绍]()
> 
> [redis zset命令大全]()

Streams
A Redis stream is a data structure that acts like an append-only log. Streams help record events in the order they occur and then syndicate them for processing. For more information, see:

Overview of Redis Streams
Redis Streams command reference
Redis Streams tutorial

> redis中的stream是一种追加型数据类型。stream可以帮助我们按照有序顺序整合数据事件进行下一步处理。想看更多，请查看
> 
> [redis streams概述]()
> 
> [redis streams命令大全]()
> 
> [redis streams指南]()

Geospatial indexes
Redis geospatial indexes are useful for finding locations within a given geographic radius or bounding box. For more information, see:

Overview of Redis geospatial indexes
Redis geospatial indexes command reference

> redis geospatial indexes对于提供的经纬度地图找到定位或者合理的路线非常有帮助。想看更多，请查看：
> 
> [redis geosptaial indexes 概述]()
> 
> [redis geosptaial命令大全]()

Bitmaps
Redis bitmaps let you perform bitwise operations on strings. For more information, see:Overview of Redis bitmaps
Redis bitmap command reference

> redis 的bitmaps允许按位操作strings。想看更多，请查看：
> 
> [redis bitmaps概览]()
> 
> [bitmap命令大全]()

Bitfields
Redis bitfields efficiently encode multiple counters in a string value. Bitfields provide atomic get, set, and increment operations and support different overflow policies. For more information, see:

Overview of Redis bitfields
The BITFIELD command.

> redis中bitfields高效地编码多位的字符串值。bitfields提供了原子性的操作get 和set，包括增量操作以及支持不同的溢出策略。想看更多，请查看：
> 
> [redis bitfields概述]()
> 
> [bitfields 命令大全]()

HyperLogLog
The Redis HyperLogLog data structures provide probabilistic estimates of the cardinality (i.e., number of elements) of large sets. For more information, see:

Overview of Redis HyperLogLog
Redis HyperLogLog command reference

> redis中HyperLoglog数据类型可以提供超大集合中元素的推算概率。想看更多，请查看：
> 
> [redis HyperLoglog概述]()
> 
> [redis HyperLOng 命令大全]()

Extensions

> 扩展

To extend the features provided by the included data types, use one of these options:

1. Write your own custom server-side functions in Lua.

2. Write your own Redis module using the modules API or check out the community-supported modules.

3. Use JSON, querying, time series, and other capabilities provided by Redis Stack.
   Redis data types tutorial

>  查看包含的数据类型扩展功能，可以通过以下途径：
> 
> 1. 通过lua脚本定制自己的函数
> 2. 通过[redis modules的API]()开发定制自己的module或者查看[社区已经支持的modules]()
> 3. 可以通过[redis stack]()查看比如JSON，querying，time series以及其他未知功能

Learning the basic Redis data types and how to use them

> 学习基本数据类型以及如何使用他们

Redis Strings
Introduction to Redis strings

Redis lists
Introduction to Redis lists

Redis sets
Introduction to Redis sets

Redis hashes
Introduction to Redis hashes

Redis sorted sets
Introduction to Redis sorted sets

Redis Streams
Introduction to Redis streams

Redis Streams tutorial
A comprehensive tutorial on Redis streams

Redis geospatial
Introduction to the Redis Geospatial data type

Redis HyperLogLog
Introduction to the Redis HyperLogLog data type

Redis bitmaps
Introduction to Redis bitmaps

Redis bitfields
Introduction to Redis bitfields
