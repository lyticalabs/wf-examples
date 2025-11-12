# README: API Reference

Welcome to the API Reference for the Workflow DevKit. This document provides a comprehensive and in-depth guide to the various packages and modules that make up the Workflow API. It is intended for developers who are building, extending, or interacting with workflows.

## Core Concepts

The API is divided into several packages, each with a specific purpose:

-   **`workflow`**: The core package that provides the fundamental primitives for building workflows.
-   **`workflow/api`**: The runtime API for interacting with workflows from outside the workflow itself.
-   **`workflow/next`**: The Next.js integration package.
-   **`@workflow/ai`**: A specialized package for building AI-powered workflows.

---

## `workflow` Package

This package contains the essential building blocks for creating workflows.

### Workflow Control and Execution

-   **`sleep(duration | date)`**: Pauses a workflow for a specified duration or until a certain date, without consuming resources. This is essential for building workflows that need to wait for a period of time before continuing.
-   **`getWorkflowMetadata()`**: Returns high-level information about the current workflow execution, such as the `workflowRunId`. This is useful for logging, tracking, and auditing purposes.
-   **`getStepMetadata()`**: Returns valuable context about the current step, including the `stepId`, retry count, and timing information. This is particularly useful for implementing idempotency.

### External Communication

-   **`fetch()`**: A specialized version of the standard `fetch` API that is designed for use within a workflow. It automatically handles serialization and provides built-in retry semantics.
-   **`createHook()`**: A low-level primitive for pausing a workflow and waiting for an arbitrary payload from an external system. This is ideal for scenarios requiring manual approval or data from a third-party service.
-   **`defineHook()`**: A utility for ensuring type safety when working with hooks. By defining the hook's payload type once, you can reuse it across your application, guaranteeing that the data sent to the hook and the data received by the workflow are always consistent.
-   **`createWebhook()`**: A higher-level abstraction for handling HTTP requests. It allows workflows to be suspended until an HTTP request is received, making them interactive and responsive to external events.

### Streaming

-   **`getWritable()`**: Provides a `WritableStream` that can be written to from both workflow and step functions, allowing you to send progress updates, logs, or any other data to an external client in real-time.

### Error Handling

-   **`FatalError`**: A specialized error type that, when thrown, will immediately stop the workflow and mark it as failed, preventing any further retries.
-   **`RetryableError`**: A specialized error type that allows you to control the retry behavior of a step with more precision than a standard `Error`, including the ability to specify a `retryAfter` duration.

---

## `workflow/api` Package

This package provides the essential functions for interacting with workflows from outside the workflow itself.

-   **`start(workflow, args)`**: The primary way to initiate a new workflow execution. It enqueues the workflow and its arguments for processing, and immediately returns a `Run` object.
-   **`getRun(runId)`**: A vital function for monitoring the status of a workflow without having to wait for it to complete. It provides immediate access to the workflow's metadata, including its current status, timing information, and any output streams.
-   **`resumeHook(token, payload)`**: The counterpart to `createHook()`, used to send a payload to a paused workflow and cause it to resume execution.
-   **`resumeWebhook(token, request)`**: The counterpart to `createWebhook()`, used to forward an HTTP `Request` to a paused workflow.

---

## `workflow/next` Package

This package provides the integration with Next.js.

-   **`withWorkflow(nextConfig)`**: The main entry point for integrating the workflow engine with your Next.js application. By wrapping your `nextConfig` with this function, you enable the necessary code transformations that allow you to use the `"use step"` and `"use workflow"` directives.

---

## `@workflow/ai` Package

This package provides specialized tools for building AI-powered workflows.

-   **`DurableAgent`**: A powerful abstraction for creating stateful, resilient, and interactive AI agents. It seamlessly integrates with the workflow engine, allowing you to define tools that are executed as durable steps with automatic retries.
-   **`WorkflowChatTransport`**: A specialized chat transport for the AI SDK that provides reliable, resumable message streaming. It's designed to work with workflow-based chat applications, automatically reconnecting to interrupted streams and ensuring that no messages are lost.


