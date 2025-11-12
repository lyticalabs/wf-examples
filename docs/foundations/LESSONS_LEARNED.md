# Lessons Learned: Foundations

This document summarizes the key takeaways from the `foundations` documentation.

- **`index.mdx`**: The `foundations` documentation provides a comprehensive overview of the core concepts of workflow programming. It covers the fundamental building blocks of workflows and steps, how to start and track workflows, common control flow patterns, error handling and retries, and how to use webhooks to respond to external events. This is a great starting point for understanding the key concepts and best practices for building robust and reliable workflows.

- **`control-flow-patterns.mdx`**: Workflows support standard JavaScript control flow patterns like sequential execution and parallel execution using `Promise.all` and `Promise.race`. This means you can orchestrate complex workflows using familiar async/await syntax, without having to learn a new DSL. This makes it easy to build sophisticated workflows that can handle a wide range of use cases, from simple data pipelines to complex, multi-step processes with timeouts and parallel branches.

- **`errors-and-retries.mdx`**: The workflow engine provides a robust error handling and retry mechanism. By default, steps are retried up to 3 times, but this can be customized using `maxRetries`. For more control, you can use `FatalError` to prevent retries and `RetryableError` to specify a custom delay. The documentation also introduces the concept of rollbacks, which is a powerful pattern for ensuring data consistency in the event of a failure.

- **`hooks.mdx`**: Hooks and webhooks are the primary mechanisms for making workflows interactive and responsive to external events. Hooks are a low-level primitive for pausing a workflow and waiting for an arbitrary payload, while webhooks are a higher-level abstraction for handling HTTP requests. The documentation provides a clear comparison of the two, and explains how to use them to build complex, event-driven workflows.

- **`idempotency.mdx`**: Idempotency is a critical concept for building reliable workflows that interact with external systems. By using the `stepId` from `getStepMetadata()` as an idempotency key, you can ensure that an operation is only performed once, even if the step is retried. This is essential for preventing duplicate side effects, such as charging a customer multiple times or sending the same email twice.

- **`serialization.mdx`**: Serialization is the process of converting data into a format that can be stored and later reconstructed. The workflow engine uses a custom serialization system that supports a wide range of types, including standard JSON types, `Date`, `RegExp`, `Map`, `Set`, and even `ReadableStream` and `WritableStream`. It's important to be aware of which types are supported, as only serializable data can be passed between workflows and steps.

- **`starting-workflows.mdx`**: The `start()` function is the entry point for executing workflows. It enqueues a workflow for execution and returns a `Run` object, which can be used to track the workflow's status, get its return value, or stream its output. The documentation highlights several common patterns, including "fire and forget" for background tasks, waiting for completion, streaming updates to the client, and checking the status of a workflow later.

- **`workflows-and-steps.mdx`**: Workflows are orchestrated by workflow functions (`"use workflow"`), which run in a sandboxed environment and are responsible for the control flow of the workflow. The actual work is done in step functions (`"use step"`), which have full access to the Node.js runtime and can be retried automatically. This separation of concerns is a fundamental concept that enables the durability and reliability of the workflow engine.
