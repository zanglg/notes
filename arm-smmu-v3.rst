
.. _smmu:

===========
ARM SMMU v3
===========

概述
====

SMMU即System Memory Management Unit，是IOMMU在ARM平台上的实现。IOMMU在系统中的
角色类似于CPU中的MMU。它服务于外设，为其提供页表转换、内存属性转换、权限检查等
服务。

.. graphviz::
   :align: center
   :caption: MMU vs IOMMU

   digraph {
     graph [bgcolor="transparent"]
     node  [shape = box, fixedsize = true, width = 2]
  
     Device -> IOMMU -> "Main Memory"
     CPU    -> MMU   -> "Main Memory"
   }

编程接口
========

SMMU提供了三种形式的软件接口，用于软件与SMMU设备进行编程，分别是:

- 位于内存中的数据结构，建立起外设与页表的对应关系
- 位于内存中的环形队列

  - Command Queue: 用于发送命令到SMMU
  - Event Queue: 用于接收事件和错误信息
  - PRI Queue: 用于接收PCIe的 `page requests`

- 硬件寄存器，其中部分只能在安全模式访问


命令
====

数据结构
========

寄存器
======

内核源码
========

虚拟化
======

.. note::
   虚拟化场景下，如果支持Stage1，GuestOS会看到一组模一样的寄存器，软件可以假
   设存一个真实的SMMU，几个数据结构和环形队列的格式也是一致的。
