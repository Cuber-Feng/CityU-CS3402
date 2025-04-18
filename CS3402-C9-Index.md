# Indexing
> Last Updated: Apr 12, 2025
## 🌳 B 树（B-tree）

- 定义：B 树是一种自平衡的多路查找树，每个节点可以有多个子节点，适合在磁盘或其他块设备上存储数据。

- 特点：
  
  - 每个节点可以存储多个键（key）和子指针（children）。
  
  - 所有叶子节点处于同一层（保持平衡）。
  
  - 所有节点的键值有序，方便范围查询。
  
  - 键和值都存在所有节点中（非叶子节点也存值）。
  
  - 插入和删除操作会保持树的平衡结构。

## 🌲 B+ 树（B+ tree）

- 定义：B+ 树是 B 树的一个变种，所有的值都存在叶子节点中，非叶子节点仅用作索引。

- 特点：
  
  - 所有实际数据都保存在叶子节点。
  
  - 非叶子节点只存储索引（key），不存储实际值。
  
  - 所有叶子节点通过指针按顺序串联，方便范围查询和顺序遍历。
  
  - 查询效率更稳定，因为只有叶子节点存值。

---

| 特性         | B 树       | B+ 树        |
| ---------- | --------- | ----------- |
| 数据存储位置     | 所有节点      | 只在叶子节点      |
| 非叶子节点是否存数据 | 是         | 否           |
| 叶子节点是否串联   | 否         | 是（链表）       |
| 范围查询效率     | 一般        | 高效（链表遍历）    |
| 访问磁盘次数     | 较少        | 稍多（必须到叶子）   |
| 应用场景       | 内存索引、较小数据 | 数据库索引、文件系统等 |

## Insert & Deletion
核心理念就是: 从下往上, 多了就拆分, 少了就合并, 具体操作可以看slide里面的demo

## 推荐 YouTube 视频
- [印度口音](https://youtu.be/aZjYr87r1b8?si=dLSITXZ2E1s5evZl)
