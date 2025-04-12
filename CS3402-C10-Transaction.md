# Transaction Management
> Last Updated: Apr 12, 2025
## 1. Concepts

- Single User vs Multiuser Systems
  
  - single-user: 同时只允许一个人访问数据库 (e.g. PC)
  
  - multiuser: 多个用户并发访问数据库 (Concurrently)

> - 因为多个用户会同时提交事务操作数据库，我们需要“事务并发控制(**transaction concurrency control**)”机制，来确保数据库在这种高并发情况下仍然保持一致和正确。
> 
> - **Transaction（事务）** 是一组操作，要么全部执行，要么全部不执行，是原子性的操作单位. 一个transaction通常有多个数据库的操作

- **Database operations**: read and write operations on a database
  
  - **Read** operation: to read the value of a data item or a group of items, e.g. SELECT
  - **Write** operation: to create a new value for a data item or a group of items, e.g. UPDATE
  - In between the read/write operations, there may be computation

- **Transaction operations**: begin and end transaction (**commit** or **abort**)
  
  - For transaction management (where to start and where to finish)
  - The new values from a transaction will become permanent only if the transaction is committed successfully

## 2. 如何提升事务处理性 (Transactio Processing Performance)

> Serial Schedule vs. Serializable Schedule

- 当多个事务在一起运行时，无论是交错执行（**interleaved**）还是一个接一个执行（**serially**），它们所有操作的执行顺序就形成了一个事务调度（**Transaction Schedule**）
- concurrent schedule (并发调度)：指的是在一个事务还没完成之前，另一个事务就已经开始执行了，也就是交错执行。
- serial schedule (串行调度)：指的是一个事务执行完以后，另一个事务才开始执行，完全没有交错，像排队一样，一个一个来。

### Consistency Problems

> Several problems can occur when concurrent transactions execute in 
> an uncontrolled manner

1. Lost Update Problem (write/ write conflicts)
2. Incorrect Summary Problem (read/write conflicts)
    一个人在算一些数据, 另一个人在修改数据

#### 👍Conflict equivalent (冲突等价):

Two schedules are said to be conflict equivalent if the 
order of any two conflicting operations (RW,WW) is the 
same in both schedule
所有发生冲突的操作对（比如读写 RW、写写 WW）的执行顺序是一样的，那这两个调度就叫做冲突等价

#### 🧱Serial schedule 串行调度:

- 一个调度 S 是串行的，意思是：每个事务 T 的所有操作在调度中是连续执行的，中间没有穿插其他事务的操作
- Serial schedules can maintain the database consistency BUT poor performance

#### ⚡Serializable schedule 可串行化调度:

- 虽然它是并发执行的（操作交错），但它与某个串行调度在“冲突顺序”上是一样的。也就是说，它的执行结果就像是某个串行调度产生的一样，所以我们认为它是“安全的”
- Can guarantee the database consistency and can have better performance.

#### 🗺️Serialization Graphs (SG, Perceduence Graph)

- 如果图中存在一条边 Ti → Tj, 则**Ti 必须在 Tj 之前执行**，否则会影响结果
- SG 是一个有向图，用来判断调度是否是“可串行化”的
- A schedule is serializable iff the SG is acyclic (无环)

## 3. Database Recovery

> 为什么需要恢复? - A Transaction may Fail
> 
> 1. computer failure (system crash)
> 2. transaction error (int overflow, 除以0)
> 3. Local errors or exception conditions detected by the transaction
> 4. Concurrency control enforcement
> 5. Disk failure
> 6. Physical problems and catastrophes(Fire)

### Recoverability Problems

#### Dirty Read Problem (write/read conflicts)

- T1 写入了 x 的值, 但是T1的后续fail, 需要充值 x, 但是又其他的 T 已经读了新 的 x

- Non-Recoverable Schedule 不能解决这个问题

### 一些标准

#### Recoverable schedule

- No committed transaction needs to be rolled back (提交过的不需要回滚)
- 如果 Ti 读了 Tj 写的数据, 那Ti 需要等Tj提交后才能提交

#### Cascadeless schedule

- Before Ti reads an item written by Tj，Tj is already committed
- 直接不允许你读那种被别人写了但是别人没提交的东西

#### Strict Schedules

- A schedule in which a transaction can neither read or write an item X until the last transaction that wrote X has committed

- 对于别人写了但是未提交的东西, 既不让你读也不让你写
