# Storage学习(一)  入门 
这篇Blog的目的就是大致的了解一下Storage会做一些什么东西，但是其实你能做的research和这个领域涉及什么似乎没有太直接的关系。

本次主要对***Information Storage & Management*** 这本书进行了学习 
## 大纲
（本次看的，将加粗标出）

* Section I: 存储系统 
	* ***Introduction***
		* 存储&历史
		* Data Center 
		* Challenges
	* Storage System 
		* Components
		* Disk Drive Components
		* Disk Drive 性能 
		* 基本原则
		* Host 的组成部分
	* 数据保护: RAID
		* RAID & Components
		* RAID 分级
		* 比较
		* RAID 的影响
	* ***智能存储系统***
		* Components
		* 智能存储阵列
		* 一个实例
* ***Section II: 存储网络技术 & 虚拟化***
	* Direct-Attached Storage & SCSI 
	* Storage Area Networks （SAN）
	* Network-Attached Storage 
	* IP SAN
	* Content-Addressed Storage
	* Storage Virtualization 
* ***Section III: Business Continuity*** 
	* What is Business Continuity 
	* Backup & Recovery
	* Local Replication
	* Remote Replication
* Section IV: 存储安全 & 管理
	* 存储设施 安全 
	* 管理存储 基础设施

## Introduction 

* 存储发展
	* RAID 
	* DAS(Direct-Attached Storage) 直接接在Cluster中的storage 
	* SAN(Storage Area Network) 基于Fibre Channel来交互，仍然是在Cluster中 
	* NAS(Network-Attached Storage) 通过网络提供 File serving 
	* IP-SAN将SAN放到了远端
* Data Center
	* 几大组成元素
		* 应用
		* Database 
		* Server and OS 
		* 网络
		* 存储阵列
	* data center 中 storage system的requirements:
		* availability 随时可方寸 
		* security 
		* scalability: storage grow with business grow  
		* performance: 性能
		* data integrity: 严格的读写规则控制？
		* capacity: 当存储的data变大，需要在同时不影响availability的前提下，提供更大的capacity
		* Managebility: 更多的自动化操作
	* 管理storage infrastructure的主要任务
		* 需要能monitor整个system
		* Reporting 相应的performance cost等 
		* 提供capacity等    这几点没有一个具象的概念是应该做些什么 
	* Manage information 的挑战：
		* 规模太大（为了确保可靠性又得depulicity）
		* 实时提供给计算 
		* 一个信息的价值是随时在变的
	* information lifecycle: 
* 智能存储系统

## Introduction to 存储网络 & 虚拟化

## Introduction to Business Continuity 

## Conclusion 

## Reference
[1] Information Storage & Management.pdf