# Parallel Computing

[TOC]

## Synchronous &  Asynchronous

Synchronous: Tasks are performed one after the other, in a sequence. Each task must be completed before the next one starts.

Asynchronous: Tasks are performed independently of each other. A task can start before the previous one is completed.

## Communication between processes

- Information channel between processes
  - Pipes: Unidirectional data channels used for communication between processes on the same machine.
  - Channel
- Communication based on a shared storage between processes
  - Shared Memory: Multiple processes can access a common memory space. Efficient but requires synchronization.
  - Redis
  - Database
- Communication based on Computer Network
  - Sockets: Enable communication between processes over a network, supporting both TCP (reliable) and UDP (unreliable) protocols.
  - Remote Procedure Calls (RPC): Allow a program to execute a procedure on another address space (commonly on a remote server).
  - HTTP
- Third-party communication services
  - Message Queues: Allow processes to exchange messages in a queue format, supporting both asynchronous and synchronous communication.

## Shared resources

### Lock mechanism

- Mutex (Mutual Exclusion): A lock that ensures only one thread can access a resource at a time. 
- Spinlock: A lock where a thread repeatedly checks for a lock to become available, "spinning" in a loop.
- Read-Write Lock: A lock that allows multiple threads to read a resource concurrently, but only one thread to write at a time.
- Semaphore: A signaling mechanism that can control access to a resource by multiple threads.
- Condition Variable: A synchronization mechanism that allows threads to wait for certain conditions to be met.
- reentrant lock

### Deadlock

Deadlock is a situation in parallel computing where two or more processes are unable to proceed because each is waiting for the other to release a resource. A deadlock situation on a resource can arise only if all of the following conditions occur simultaneously in a system.

- Mutual exclusion: multiple resources are not shareable; only one process at a time may use each resource.

- Hold and wait or resource holding: a process is currently holding at least one resource and requesting additional resources which are being held by other processes.
- No preemption: a resource can be released only voluntarily by the process holding it.
- Circular wait: each process must be waiting for a resource which is being held by another process, which in turn is waiting for the first process to release the resource.



## Task Assignment: Load Balancing

### Amdahl’s Law & Gustafson’s Law