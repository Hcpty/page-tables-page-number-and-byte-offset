# Readme
A note about Byte Addressing.

### 从页的序号到页的物理地址的映射

可以把一个文件分成很多个页，每一个页都有一个序号，从0开始。当把该文件存储在磁盘中时，每一个页号都对应一个磁盘地址。当把该文件存储在主存中时，每一个页号都对应一个主存地址。可以用一张表建立从页号到对应的物理地址的映射，这个表称为页表。当需要读取某一个文件的某一个页的内容的时候，可以根据页号到该文件对应的页表中查询对应的物理地址。

### 字节的物理地址的计算公式

一个页中通常包含2<sup>p</sup>个字节，每一个字节都有一个逻辑地址。字节的逻辑地址的数据结构中包含两个字段：
- 该字节所在的页的页号，可以根据页的序号从页表中查询对应的页的物理地址。
- 该字节在该页中的偏移字节数。

字节的物理地址 = 该字节所在的页的物理地址 + 该字节在该页中的偏移字节数

借助该计算公式，MMU (Memory Management Unit) 可以执行从逻辑地址到物理地址的翻译。

### 有层次的序号

页的序号可以是有层次的，形如abcde...m，其中a代表1级序号，b代表2级序号，以此类推。根据有层次的序号从页表中查询对应的页的物理地址的过程如下：

```
根据页的1级序号从1级页表中查询到的不是该页的物理地址，而是2级页表的物理地址；
根据页的2级序号从2级页表中查询到的也不是该页的物理地址，而是3级页表的物理地址；
根据页的3级序号从3级页表中查询到的也不是该页的物理地址，而是4级页表的物理地址；
……
根据页的m级序号从m级页表中查询到该页的物理地址；
```

### Credits
- Computer Systems: A Programmer's Perspective, Third Edition - Randal E. Bryant and David R. O'Hallaron
