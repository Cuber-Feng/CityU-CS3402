# File Organization

> Last Updated: Apr 12, 2025
## 一些简单的东西
Data Abstraction: 3-level architecture

Storage Medium for Databases

Memory Hierarchy

Disk Storage Devices

Double Buffer to Reduce Access Delay

## Records

1. **Fixed length** records:
   
   - Every record in the file has exactly the same size (in bytes)

2. **Variable length** records:
   
   - If different records in the file have different sizes
   
   - Separator characters or length fields are needed so that the record can be “parsed” (因为长度不一样, 所以需要分隔符或者额外一个记录每段长度的文件)

## Files of Records

### 1. Database: data file (records) + meta-data

一个数据库本质上包含两部分：

- **数据文件（Data File）**：真正保存数据的部分，例如一张表中的学生记录。

- **元数据（Meta-data）**：描述数据结构的信息，例如每一列的名字、数据类型等。

### 2. A data file (e.g., table) is a sequence of records (e.g., tuples), where each record is a collection of data values (fields)

一个数据文件（例如表）是一串记录（例如元组）的集合，其中每条记录是一组数据值（字段）

### 3. A file descriptor (or file header) includes information that describes the file, such as the field names and their data types, and the addresses of the file blocks on disk

一个文件描述符（或文件头）包含描述该文件的信息，比如字段名、数据类型、以及该文件在磁盘上各个数据块的地址。

```mathematica
📁 数据文件（Data File）
├── 📄 文件头（File Descriptor）
│   ├── 字段名称和类型（ID: int, Name: string...）
│   └── 文件块地址列表（在哪些磁盘块上）
└── 📑 数据记录（Records）
    ├── Record 1: [ID=1, Name=Tom, Age=20...]
    ├── Record 2: ...
```

### 4. Block & Record

> **Block** 是 **磁盘上的最小读写单位**
> 
> 当数据库从磁盘读数据时，它不是一条记录一条记录地读，而是**一整块（block）地读写**，这样效率更高
> 
> 通常是 512B、1024B、4096B 等

1. 当块大小（block size）大于记录大小（record size）时，一个块可以存储多条记录

2. 假设 block 的大小是 B 字节，记录大小是 R 字节，并且 B ≥ R, 每个block最多可以放 floor(B/R) 条 records

3. Blocking (块存储)：指的是把多条记录存储到一个磁盘块中。

4. Blocking factor（bfr, 块因子) 是每个块中可以存储的记录条数

5. File records 可以是 spanned 或 unspanned
   
   1. spanned: 一个record可以被拆分到两个block里 (非固定长度的记录可以用这个来避免浪费空间)
   
   2. unspanned: 一个record必须再一个block内 (固定长度的记录通常用这个)

### 5. Typical Operations on Files

OPEN/ FIND/ FINDNEXT/ READ/ READ_ORDERED/ INSERT/ DELETE/ REORGANIZE/ MODIFY/ CLOSE

* REORGANIZE: reorganizes the file records. For example, the records marked “deleted” are physically removed from the file or a new organization of the file records is created

### 6. Unordered Files

1. 也叫heap file

2. 新的record插在文件末尾 (插入很高效)

3. 需要linear search(从头找到尾)

### 7. Ordered Files

1. 也叫 sequential file

2. record 通过 values of an ordering field 来保持有序

3. 按这个ordering field 来读取特别高效

4. 适用二分查找

5. 插入很expensive
   
   - 通常会为新记录保留一个单独的无序溢出文件，以提高插入效率；该文件会定期与主有序文件合并。

## Extendible and Dynamic Hashing
