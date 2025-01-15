# Service design
[TOC]

## Context

- **Request**: The system receives input data from the user. This input could be a query, command, or data that needs to be processed.
- **Response**: After the process is completed, the system generates a response based on the results.
- **Context**: The input is first translated into the internal language of the service. This internal language is used to ensure that the input is standardized and can be understood and processed consistently across various system components.
- **Process**: Based on the translated input, the system determines the appropriate process or workflow to handle the request. Analyze Input Type, Select Process, Invoke Process, Process Execution.

![图片1](assets/图片1.svg)

## Creating objects

### Singleton

Singleton refers to ensures a class has only one global instance and provides a global access entrance of access to that instance. The key to building a singleton including: 

- Restrict the constructor's visibility to prevent external creation of new instances, ensuring that instances are created only at expected and unique times, such as during the first access or system initialization.
- Provide a centralized global access point to guarantee that the singleton instance can be accessed consistently from anywhere.

### Factory

Factory determines the type of instance to create based on input, maintaining a $\text{key} \to \text{instance}$ mapping table that associates each key with its corresponding instance constructor.

## Combining objects

### Adapter

Adapter allow incompatible interfaces to work together that could not interact directly. 

### Decorator

Decorator adds one or more layers of functionality to a base class without modifying the class itself. Both the decorator and the decorated object adhere to the same interface, ensuring that the client remains unaware of the decorator's presence.

## Manage objects

### Pool

Pool manages an object pool that stores reusable objects to optimize resource usage and performance by reusing objects. Pool is suitable for objects that be created and destroyed frequently. Specifically, a pool initially creates and initializes a set number of objects. When required, an available object is obtained from the pool, and after use, it is returned for reuse. If the pool's objects are exhausted or there are too many unused objects, the pool dynamically adjusts by creating or destroying objects.