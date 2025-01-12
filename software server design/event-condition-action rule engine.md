# Event-Condition-Action Rule Engine

[TOC]

## Architecture

An Event-Condition-Action (ECA) rule engine is a framework used in event-driven systems to automate responses based on specific conditions.

- **Event**: A trigger that initiates the rule. It can be anything from a user action, a system event, or a message received.
- **Condition**:  A set of criteria that must be met for the action to be executed. If the condition evaluates to true, the action is triggered.
- **Action**: The operation or set of operations that are executed when the event occurs and the condition is met.

![ECA](assets/ECA.svg)

- **Event Manager**: 负责捕获和处理系统中的事件。
- **Condition Evaluator**: 负责根据预定义的条件评估事件是否满足执行条件。
- **Action Executor**: 当条件满足时，负责执行相应的动作。
- **Rule Repository**: 存储所有的 ECA 规则。
- **Logging System**: 记录事件的触发、条件的评估和动作的执行情况。

## Event Manager

- **Event Capture**: 捕获来自各种来源的事件。
- **Event Queue**: 用于缓冲事件，确保高吞吐量和低延迟。
- **Event Dispatcher**: 将事件分发到相应的处理器。
- **Event Handlers**: 执行具体的事件处理逻辑。
- **Error Handling**: 确保在事件处理过程中发生错误时能够优雅地恢复。

## Condition Evaluator

- **Rule script definition**: Define rules using a format that is easy to understand and modify, such as JSON or a DSL (Domain Specific Language).
- **Rule Parser**: Parses user-defined rule scripts into internal data structures that can be used by the condition engine.
- **Data Retrieval**: Retrieve the necessary field values from the event object using the dictionary or object accessors.
- **Condition Engine**: Implement conditional operations based on Boolean logic, expression calculation, etc.
- **Caching**: Cache the results of evaluated conditions to improve performance.

## Action Executor

- **Action Definitions**: 定义所有可能的动作及其参数。
- **Action Execution Scheduler**: 调度和管理动作的执行。
- **Action Handlers**: 执行具体的动作逻辑。
- **Error Handling**: 确保在执行动作过程中发生错误时能够优雅地恢复。
