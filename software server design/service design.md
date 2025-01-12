# Service design
[TOC]

## Context

- **Request**: The system receives input data from the user. This input could be a query, command, or data that needs to be processed.
- **Context**: The input is first translated into the internal language of the service. This internal language is used to ensure that the input is standardized and can be understood and processed consistently across various system components.
- **Process**: Based on the translated input, the system determines the appropriate process or workflow to handle the request. Analyze Input Type, Select Process, Invoke Process, Process Execution.
- **Respond**: After the process is completed, the system generates a response based on the results.

![图片1](assets/图片1.svg)