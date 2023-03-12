---
title: redis_string_command
date: 2023-03-09 22:35:04
tags: redis
comments: true
categories:
- redis
- 文档翻译
- 原创
about: 中间件
---

APPEND
Syntax
APPEND key value
Available since:
2.0.0
Time complexity:
O(1). The amortized time complexity is O(1) assuming the appended value is small and the already present value is of any size, since the dynamic string library used by Redis will double the free space available on every reallocation.
ACL categories:
@write, @string, @fast
If key already exists and is a string, this command appends the value at the end of the string. If key does not exist it is created and set as an empty string, so APPEND will be similar to SET in this special case.
<!--more-->
Return
Integer reply: the length of the string after the append operation.

Examples
redis> EXISTS mykey
(integer) 0
redis> APPEND mykey "Hello"
(integer) 5
redis> APPEND mykey " World"
(integer) 11
redis> GET mykey
"Hello World"
redis> 
Pattern: Time series
The APPEND command can be used to create a very compact representation of a list of fixed-size samples, usually referred as time series. Every time a new sample arrives we can store it using the command

APPEND timeseries "fixed-size sample"
Accessing individual elements in the time series is not hard:

STRLEN can be used in order to obtain the number of samples.
GETRANGE allows for random access of elements. If our time series have associated time information we can easily implement a binary search to get range combining GETRANGE with the Lua scripting engine available in Redis 2.6.
SETRANGE can be used to overwrite an existing time series.
The limitation of this pattern is that we are forced into an append-only mode of operation, there is no way to cut the time series to a given size easily because Redis currently lacks a command able to trim string objects. However the space efficiency of time series stored in this way is remarkable.

Hint: it is possible to switch to a different key based on the current Unix time, in this way it is possible to have just a relatively small amount of samples per key, to avoid dealing with very big keys, and to make this pattern more friendly to be distributed across many Redis instances.

An example sampling the temperature of a sensor using fixed-size strings (using a binary format is better in real implementations).

redis> APPEND ts "0043"
(integer) 4
redis> APPEND ts "0035"
(integer) 8
redis> GETRANGE ts 0 3
"0043"
redis> GETRANGE ts 4 7
"0035"
redis> 

DECR
Syntax
DECR key
Available since:
1.0.0
Time complexity:
O(1)
ACL categories:
@write, @string, @fast
Decrements the number stored at key by one. If the key does not exist, it is set to 0 before performing the operation. An error is returned if the key contains a value of the wrong type or contains a string that can not be represented as integer. This operation is limited to 64 bit signed integers.

See INCR for extra information on increment/decrement operations.

Return
Integer reply: the value of key after the decrement

Examples
redis> SET mykey "10"
"OK"
redis> DECR mykey
(integer) 9
redis> SET mykey "234293482390480948029348230948"
"OK"
redis> DECR mykey
(error) value is not an integer or out of range
redis> 

DECRBY
Syntax
DECRBY key decrement
Available since:
1.0.0
Time complexity:
O(1)
ACL categories:
@write, @string, @fast
Decrements the number stored at key by decrement. If the key does not exist, it is set to 0 before performing the operation. An error is returned if the key contains a value of the wrong type or contains a string that can not be represented as integer. This operation is limited to 64 bit signed integers.

See INCR for extra information on increment/decrement operations.

Return
Integer reply: the value of key after the decrement

Examples
redis> SET mykey "10"
"OK"
redis> DECRBY mykey 3
(integer) 7
redis> 

GET
Syntax
GET key
Available since:
1.0.0
Time complexity:
O(1)
ACL categories:
@read, @string, @fast
Get the value of key. If the key does not exist the special value nil is returned. An error is returned if the value stored at key is not a string, because GET only handles string values.

Return
Bulk string reply: the value of key, or nil when key does not exist.

Examples
redis> GET nonexisting
(nil)
redis> SET mykey "Hello"
"OK"
redis> GET mykey
"Hello"
redis> 


GETDEL
Syntax
GETDEL key
Available since:
6.2.0
Time complexity:
O(1)
ACL categories:
@write, @string, @fast
Get the value of key and delete the key. This command is similar to GET, except for the fact that it also deletes the key on success (if and only if the key's value type is a string).

Return
Bulk string reply: the value of key, nil when key does not exist, or an error if the key's value type isn't a string.

Examples
redis> SET mykey "Hello"
"OK"
redis> GETDEL mykey
"Hello"
redis> GET mykey
(nil)
redis> 

GETEX
Syntax
GETEX key [EX seconds | PX milliseconds | EXAT unix-time-seconds |
  PXAT unix-time-milliseconds | PERSIST]
Available since:
6.2.0
Time complexity:
O(1)
ACL categories:
@write, @string, @fast
Get the value of key and optionally set its expiration. GETEX is similar to GET, but is a write command with additional options.

Options
The GETEX command supports a set of options that modify its behavior:

EX seconds -- Set the specified expire time, in seconds.
PX milliseconds -- Set the specified expire time, in milliseconds.
EXAT timestamp-seconds -- Set the specified Unix time at which the key will expire, in seconds.
PXAT timestamp-milliseconds -- Set the specified Unix time at which the key will expire, in milliseconds.
PERSIST -- Remove the time to live associated with the key.
Return
Bulk string reply: the value of key, or nil when key does not exist.

Examples
redis> SET mykey "Hello"
"OK"
redis> GETEX mykey
"Hello"
redis> TTL mykey
(integer) -1
redis> GETEX mykey EX 60
"Hello"
redis> TTL mykey
(integer) 60
redis> 

GETRANGE
Syntax
GETRANGE key start end
Available since:
2.4.0
Time complexity:
O(N) where N is the length of the returned string. The complexity is ultimately determined by the returned length, but because creating a substring from an existing string is very cheap, it can be considered O(1) for small strings.
ACL categories:
@read, @string, @slow
Returns the substring of the string value stored at key, determined by the offsets start and end (both are inclusive). Negative offsets can be used in order to provide an offset starting from the end of the string. So -1 means the last character, -2 the penultimate and so forth.

The function handles out of range requests by limiting the resulting range to the actual length of the string.

Return
Bulk string reply

Examples
redis> SET mykey "This is a string"
"OK"
redis> GETRANGE mykey 0 3
"This"
redis> GETRANGE mykey -3 -1
"ing"
redis> GETRANGE mykey 0 -1
"This is a string"
redis> GETRANGE mykey 10 100
"string"
redis> 










