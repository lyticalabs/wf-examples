# README: Workflow Foundations

Welcome to the Foundations guide for the Workflow DevKit. This document provides an in-depth overview of the core concepts that you need to understand to build robust and reliable workflows.

## Core Concepts

### Workflows and Steps

-   **Workflows**: Orchestrated by workflow functions (`"use workflow"`), which run in a sandboxed environment and are responsible for the control flow of the workflow. They are deterministic and can be replayed.
-   **Steps**: The actual work is done in step functions (`"use step"`), which have full access to the Node.js runtime and can be retried automatically.

This separation of concerns is a fundamental concept that enables the durability and reliability of the workflow engine.

### Starting and Tracking Workflows

-   The `start()` function is the entry point for executing workflows. It enqueues a workflow for execution and returns a `Run` object, which can be used to track the workflow's status, get its return value, or stream its output.
-   Common patterns for starting workflows include "fire and forget" for background tasks, waiting for completion, streaming updates to the client, and checking the status of a workflow later.

### Control Flow

-   Workflows support standard JavaScript control flow patterns like sequential execution and parallel execution using `Promise.all` and `Promise.race`. This means you can orchestrate complex workflows using familiar async/await syntax.

### Error Handling and Retries

-   The workflow engine provides a robust error handling and retry mechanism. By default, steps are retried up to 3 times, but this can be customized using `maxRetries`.
-   For more control, you can use `FatalError` to prevent retries and `RetryableError` to specify a custom delay.
-   The documentation also introduces the concept of **rollbacks**, which is a powerful pattern for ensuring data consistency in the event of a failure.

### Interacting with External Systems

-   **Hooks and Webhooks**: These are the primary mechanisms for making workflows interactive and responsive to external events. Hooks are a low-level primitive for pausing a workflow and waiting for an arbitrary payload, while webhooks are a higher-level abstraction for handling HTTP requests.
-   **Idempotency**: A critical concept for building reliable workflows that interact with external systems. By using the `stepId` from `getStepMetadata()` as an idempotency key, you can ensure that an operation is only performed once, even if the step is retried.

### Serialization

-   All data passed between workflows and steps must be serializable. The workflow engine uses a custom serialization system that supports a wide range of types, including standard JSON types, `Date`, `RegExp`, `Map`, `Set`, and even `ReadableStream` and `WritableStream`.


