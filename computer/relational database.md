# Relational Database

[TOC]

## Database Paradigm

- 1NF: **Ensures the Atomicity of Each Column**
- 2NF: **Non-Key Attributes Are Fully Dependent on the Primary Key**
- 3NF: **No Non-Key Attribute Depends on Another Non-Key Attribute**

## Transactions

### Principles 

* **Atomicity**: ensures that a transaction is treated as a single, indivisible unit of work. Either all the changes made by the transaction are applied, or none of them are. If any part of the transaction fails, the entire transaction is rolled back, and the database remains unchanged. 

* **Consistency**: ensures that a transaction takes the database from one consistent state to another. If a transaction violates these rules, it will be rejected, and the database will remain unchanged.

* **Isolation**: ensures that concurrent transactions do not interfere with each other. This prevents issues like dirty reads, non-repeatable reads, and phantom reads. 

* **Durability**: guarantees that once a transaction is successfully completed, its changes are permanently saved and will survive any subsequent system failures, such as power outages or crashes.

### Isolation Level

Problem:

- **Dirty reads**: occurs when one transaction reads data that is being modified by another transaction that hasn't been committed yet, such as rolling back one transaction and affecting another.
- **Non-repeatable reads**: occur when a transaction reads a piece of data and, while the transaction is still active, another transaction modifies or deletes that same piece of data and commits the change. 
- **Phantom reads**: happen when a transaction reads a set of rows that satisfy a certain condition, but while the transaction is still active, another transaction inserts, updates, or deletes rows that match that condition, causing the initial transaction to see a different set of rows when it reads again.

Solution:

1. **READ-UNCOMMITTED**: This is the lowest isolation level. Transactions can read data modified by other transactions that haven't been committed yet. It can lead to dirty reads, non-repeatable reads, and phantom reads.
2. **READ-COMMITTED**: Transactions can only read committed data. It prevents dirty reads but may still lead to non-repeatable reads and phantom reads.
3. **REPEATABLE-READ**: This level ensures that data read by a transaction will not change until the transaction is complete. It uses locks to maintain consistency, preventing even committed updates from affecting the transaction. Non-repeatable reads are prevented, but phantom reads (new rows appearing) can still occur.
4. **SERIALIZABLE**: This is the highest isolation level. Transactions are fully isolated from each other. It prevents dirty reads, non-repeatable reads, and phantom reads, but can also cause higher contention and performance issues due to locking.

***Q: Non-repeatable reads vs. Phantom reads?***

Non-repeatable reads focus on modification, and phantom reads focus on adding or deleting rows.

### MVCC

#### Undo Log

The Undo Log is a record of the actions performed on the database. It stores the old values of data that have been modified by a transaction. In the event of a rollback or a transaction failure, the Undo Log is used to revert the changes made by the transaction to maintain consistency and integrity of the data.

#### Redo Log

The Redo Log is a record of the changes made to the database. It contains a history of all modifications made to the database's data files, such as inserts, updates, and deletes. The Redo Log is used for database recovery in case of a crash. By replaying the actions recorded in the Redo Log, the system can reapply the changes to bring the database back to a consistent state.

#### ReadView

当一个事务开始时，MySQL 会为该事务创建一个 "ReadView"。这个 ReadView 记录了事务启动时数据库中的数据版本。对于每个事务，它只能看到在事务启动时已经提交的数据，而对于尚未提交的数据，它将看不到。这就确保了事务之间的隔离性。



行级锁是另一种并发控制机制，它与 MVCC 不同。行级锁允许事务锁定数据库表中的特定行，以防止其他事务修改这些行。这种锁定机制在写入操作时特别有用，因为它可以确保事务之间的数据不会被相互干扰。



因此，ReadView 机制和行级锁在 MySQL 中是并行使用的。ReadView 机制主要用于读取操作，而行级锁则用于写入操作。它们共同确保了事务之间的隔离性和一致性，同时允许并发操作。

#### Bin Log

The Binary Log is a detailed record of all changes made to the database, including statements that modify data (such as INSERT, UPDATE, DELETE) and structural changes (such as ALTER TABLE). Unlike the Redo Log, which is used for crash recovery, the Binary Log serves other purposes such as replication, auditing, and point-in-time recovery. It is used to replicate changes from the master database to one or more slave databases in MySQL's replication setup.

### Locks

* Shared locks
* Exclusive locks
* Update locks

#### Lock Granularity  

* Table Locks
* Row Locks
  * MCVV, Multi-Version Concurrency Control


## Index

### B+ Tree Index

<img src="./assets/bplustreefull-3-1024x301.png" alt="img" style="zoom: 33%;" />

***Q: B Tree vs. B+ Tree?***

- Structure and Nodes:
  - B Tree: In a B tree, each node can have multiple keys and child pointers.
  - B+ Tree: In a B+ tree, keys are only stored in the leaf nodes. It makes the search more efficient since we can store more keys in internal nodes – this means we need to access fewer nodes.
- Leaf nodes in a B+ tree are linked together making range search operations efficient and quick.

[MySQL](./mysql.md)