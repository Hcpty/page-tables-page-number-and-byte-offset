# Readme
A note about Page Table.

### 从页的序号到页的物理地址的映射

一个文件可以分为很多页，每一个页都有一个序号，从0开始，当把该文件存储在磁盘中时，每一个页都有一个磁盘地址，当把该文件存储在主存中时，每一个页都有一个主存地址。可以用一张表把每一个页的序号和每一个页的物理地址关联起来，把这个表称为页表。当需要读取该文件的某一个页的内容的时候，就根据页的序号从页表中查询对应的页的物理地址。

### 字节的物理地址的计算公式

一个页中通常包含2<sup>p</sup>个字节，每一个字节都有一个地址，字节的地址的数据结构有两个字段：
- 字节所在的页的序号，可以根据页的序号从页表中查询对应的页的物理地址。
- 字节在该页中的偏移字节数。

字节的物理地址 = 页的物理地址 + 该字节在该页中的偏移字节数

借助页表和字节的物理地址的计算公式，Memory Management Unit可以完成从 (页的序号, 字节的偏移量) 到字节的物理地址的转换。

### 有层次的序号

页的序号可以是有层次的，形如abcde...m，其中a代表1级序号，b代表2级序号，以此类推。对于有层次的序号，查询对应的页的物理地址的过程如下：

```
根据页的1级序号从1级页表中查询到的不是该页的物理地址，而是2级页表的物理地址；
根据页的2级序号从2级页表中查询到的也不是该页的物理地址，而是3级页表的物理地址；
根据页的3级序号从3级页表中查询到的也不是该页的物理地址，而是4级页表的物理地址；
……
根据页的m级序号从m级页表中查询到该页的物理地址；
```

这种做法增加了查询次数，但是好处是每级页表的尺寸都可以很小，从而减少了初次建立页表的开销。

### Credits
- Computer Systems: A Programmer's Perspective, Third Edition
- [Multilevel Paging in Operating System - GeeksforGeeks](https://www.geeksforgeeks.org/multilevel-paging-in-operating-system/)
