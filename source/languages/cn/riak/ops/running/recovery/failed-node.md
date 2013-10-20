---
title: Recovering a Failed Node
project: riak
version: 1.4.2+
document: cookbook
toc: true
audience: advanced
keywords: [troubleshooting]
---

节点失效后重启会花费比常规启动更长的时间。启动时间过长还会导致其他问题。为了避免在
恢复节点时出现问题，应该按照下面介绍的技术进行操作。

## 一般性恢复

要恢复一个节点，根据具体的失效情况，可以使用一些基本的原则，检查 RAID 和文件系统的一致性，
错误记忆，完整的网络连接等。

一般而言，要让失效的节点重新上线，必须保证使用和失效前一样的节点名。如果名字不一样，集群会
认为这是一个全新的节点，失效的节点还是环的一部分，
除非手动执行 `riak-admin remove riak@node-name.host` 命令将其删除。


恢复节点时，会进行提示移交操作，同时还会从集群的其他节点中获取更新的数据。集群可能会对正在
移交的数据返回“not found”响应（详细信心请阅读“[[最终一致性|Eventual Consistency]]”一文，
介绍当失效节点还没加入集群时，系统应该如何响应）。

根据存储后台的不同，可能还要做其他操作。

## Bitcask

使用 Bitcask 后台的失效节点可以使用 `riak start` 或者 Riak 的 init.d 脚本启动，而且
可以进行自我修复。

详细内容请阅读 [[Failure and Recovery]] 一文。