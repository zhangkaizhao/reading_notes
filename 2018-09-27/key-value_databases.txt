# Key-value databases

2018-09-27

Source:

key / value 数据库的选型
https://www.keakon.net/2018/07/13/key%20/%20value%20%E6%95%B0%E6%8D%AE%E5%BA%93%E7%9A%84%E9%80%89%E5%9E%8B
(2018-07-13)

Prelude:

* in memory: Redis
* in disk on single machine: RocksDB
* over TB level: Cassandra, HBase, etc.

LMDB issue: using B+ tree and that results in bad performance of random write.

Summary:

For about several tens of GB to several hundreds of GB level and using Go language, BadgerDB is a good choice.
And without BadgerDB, RocksDB is the only choice now.
