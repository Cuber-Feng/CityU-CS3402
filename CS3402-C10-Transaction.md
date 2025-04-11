# Transaction Management

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


