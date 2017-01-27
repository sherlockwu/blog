# Logging/ Journaling （write-ahead logging）
## 根本原因：
* crash 的时候会导致disk中一些状态（例如，inode和文件）不一致， 需要在recover的时候检验并恢复
* fsck 检查disk状态 很慢
* 使用journaling 记录操作（metadata &/or data） （也要防止在写journaling的时候crash，需要checksum）

## journal 的方法：
* physical journal: journal 中记录下一次改变后的data
    * 只记录对metadata的操作 （因为对data操作，没法记录啊，就是physical journaling）
* 然后再将数据写到确定的位置上（checkpointing）
* Recovery:
    * 重新将log中的内容写到disk上就可以
* Batch Log updates     
    * buffer writes, 所以也合并这些log
* Reuse log space:
    * journal super block 记录head和tail journal， 其他的可以被reuse
* metadata journaling
    * 不写data change 到log， 只写metadata
* 

##  copy-on-write
* LFS 就是一种 cow

## log-structured file system
* 整个 file system 就是log， log是按顺序排序的一系列file的集合
* （包括metadata）buffer写在mem，然后一次性sequential写
* 

## Backpointer (每个block有一个回指inode的指针)


