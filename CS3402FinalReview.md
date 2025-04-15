# FinalReview
> Last Updated: Apr 15, 2025

## C1 数据库和ER的概念
- ER的具体画法(weak entity, partial key, Role Indicators, derived attribute(通过其他的attributes计算得到))

## C2 ER & Relational Model
- (min, max) notation
- Relationship of Higher Degree (3个实体的联系)
- 从ER到Relational
  1. Map **strong entity** type into **relation**
  2. Map **weak entity** + identifying relationship type into **relation** + foreign key 
  3. Map binary **1:1** relationship types into **attributes** (foreign key approach)
  4. Map binary **1:N(N:1)** Relationship types into **attributes** (foreign key approach)
  5. Map binary **M:N** relationship type into **relation + foreign key** (cross reference approach)
  6. Map **N-ary** relationship type into **relation** (cross reference approach)
  7. Map **multi-valued attribute** into **relation** + foreign key

## C3 Integrity Constraints

- Domain constraints
- Key constraints
- Entity integrity constraints
- Referential integrity constraints

- Functional Dependency
- Closure of FDs
  - Equivalence of Sets of FDs
- Closure of attribute set
  - super key & candidate key

## C4 Normal Forms
- 1st normal form
  - All attributes are simple (no composite or multivalued attributes)
- 2nd normal form
  - All non-prime attributes depend on the whole key (no partial dependency)
- 3rd normal form 
  - All non-prime attributes only depend on the key (no transitive dependency)

- 找到所有的候选键再判断NF
- Normalization

## C5&6 SQL
- **DQL**
  - SELECT -> FROM -> WHERE -> GROUP BY -> HAVING -> ORDER BY
  - Set operations: UNION, INTERSECT, MINUS/EXCEPT
  - Nested queries: IN, ANY/SOME, ALL
  - Correlated Nested Queries 每一个外面的行, 都需要跑一边内部的query): EXIST
- DML
- DDL
  - Create Table, Delete table,, update table
  - CREATE/DROP Index
  - Views (Virtual Tables)
 
## C7 Relational AlgebraUnary 
- Unary Relational Operations
 SELECT (symbol: (sigma))
 PROJECT (symbol: (pi))
 RENAME (symbol: (rho))
 Binary Relational Operations
- Binary Relational Operations
 JOIN (several variations of JOIN exist)
 DIVISION
- from set theory
 UNION ( ), INTERSECTION ( ), DIFFERENCE (or MINUS, – )
 CARTESIAN PRODUCT ( x)
- Additional Relational Operations
 AGGREGATE FUNCTIONS (These compute summary of 
information: for example, SUM, COUNT, AVG, MIN, MAX)
(还有)

## C8 Files & Hashed Files
- 不能只读一个record, 读的最小单位是block
- Blocking factor (bfr) floor function
- unspanned or spanned
- Unordered Files/heap file & Ordered Files/sequential file
- Collision Resolution
- Extendible and Dynamic Hashing: 只有directory有区别, 一个是array, 一个是tree

## C9 Indexing Techniques
- Single Level Indexes
- Multi-Level Indexes (static)
- B tree Index 
- B+ tree Index
  - degree是有多少个pointer 而不是key

## C10  Transaction Management
- Schedule
  - Serial schedule & Concurrent schedule & Serializability
  - Serialization Graphs
- Recoverability
  - Non-Recoverable
  - Recoverable
  - Cascadeless
  - Strict
- ACID Properties of Transactions
  - Atomicity(原子): A transaction is an atomic unit of processing. It is either performed completely or not performed at all (all or nothing)
  - Consistency: A correct execution of a transaction must take the database from one consistent state to another (correctness)
  - Isolation: A transaction should not make its updates visible to other transactions until it is committed (no partial results)
  - Durability: Once a transaction changes the database state and the changes are committed, these changes must never be lost because of subsequent failure (committed and permanent results)

## C11 Concurrency Control (还没学!!!)
- Basic Two Phase Locking (B2PL)
- **S2PL**, C2PL
- 用来: Guarantee Serializablity, Guarantee Recoverability, Prevent Deadlock
- 死锁
  - Wait-die Rule
  - Wound-Wait Rule
  - detection and resolution
