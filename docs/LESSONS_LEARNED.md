# The Ultimate Lessons Learned: Workflow DevKit

This document synthesizes the most critical takeaways, best practices, and non-obvious insights from across the entire Workflow DevKit documentation **and our verified example projects**. It is intended to be a high-density guide for developers and AI agents to build robust, resilient, and efficient workflows.

---

## 1. Core Principles & Architecture

-   **Separation of Concerns is Everything**: The fundamental concept is the split between **workflows (`"use workflow"`)** and **steps (`"use step"`)**.
    -   **Workflows** are for *orchestration*. They run in a sandboxed, deterministic environment. They manage control flow (`Promise.all`, `if/else`, loops) but cannot perform side effects like I/O or use native Node.js modules.
    -   **Steps** are for *execution*. They run in a full Node.js environment and handle all side effects: API calls, database queries, file system access, etc.
    -   *Lesson*: Never put side-effect-producing code in a workflow function. Always move it to a step. This separation is the key to durability and replayability.

-   **Directives are the Magic**: The `"use workflow"` and `"use step"` directives are not comments. They are compile-time signals that trigger code transformation, separating the orchestration logic from the executable steps. This is how the devkit achieves its durability.
    -   *Lesson*: Your entire setup hinges on these directives being present and your build process (e.g., `withWorkflow()` in Next.js) being correctly configured to recognize them.

-   **Serialization is the Contract**: All data passed as arguments or returned as values between workflows and steps *must* be serializable.
    -   The devkit supports many types beyond JSON (Dates, Maps, Sets, Streams), but not functions, class instances, or other complex objects.
    -   *Lesson*: Pass plain data. If you need a class instance inside a step, pass the constructor arguments and instantiate it within the step.

---

## 2. Building Resilient Workflows

-   **Idempotency is Not Optional**: Steps can be retried automatically. To prevent duplicate side effects (e.g., charging a card twice), you must make your steps idempotent.
    -   *Lesson*: Use `getStepMetadata()` to get the unique `stepId` and pass it as an idempotency key to any external API that supports it. This is the most reliable way to ensure an operation runs exactly once.

-   **Master Error Handling**: The default retry mechanism (3 times) is good, but for robust workflows, you need more control.
    -   `FatalError`: Use this for unrecoverable errors (e.g., invalid input, 4xx API errors). It stops retries immediately and fails the workflow.
    -   `RetryableError`: Use this for transient errors where you need a custom delay (e.g., rate limiting). You can specify `retryAfter`.
    -   *Lesson*: Don't rely on generic `try/catch`. Use `FatalError` and `RetryableError` to give the workflow engine precise instructions on how to handle failures.

-   **`fetch` is Special**: The `fetch` you use inside a workflow is a built-in step function, not the global one.
    -   It automatically handles serialization and has built-in retry logic.
    -   *Lesson*: If you need to use a library (like the AI SDK) that relies on the global `fetch`, you must explicitly provide it at the start of your workflow: `globalThis.fetch = fetch`.

---

## 3. Asynchronous & Interactive Workflows

-   **Hooks for Human-in-the-Loop**: `createHook()` is the primitive for pausing a workflow to wait for external input. This is for manual approvals, callbacks, or any process that can't be completed in a single run.
    -   `defineHook()`: Always use this to create strongly-typed hooks. It improves type safety and allows for schema validation, preventing invalid data from ever reaching your workflow.
-   **Webhooks for External Systems**: `createWebhook()` is a higher-level abstraction for pausing a workflow until it receives an HTTP request. It's perfect for integrating with third-party services (GitHub, Stripe, etc.).
    -   *Lesson*: When using `respondWith: "manual"`, you are responsible for calling `request.respondWith()`. Ensure every code path, especially error paths, sends a response to avoid leaving the HTTP request hanging.

-   **`sleep()` is Resource-Free**: The `sleep()` function is a durable timer. It pauses the workflow without consuming any server resources, making it cheap and efficient for long delays.

---

## 4. AI & Streaming

-   **`DurableAgent` for Resilient AI**: The `@workflow/ai` package is essential for AI work. `DurableAgent` creates stateful AI assistants where tools are executed as durable, retryable steps.
    -   *Lesson*: This is the canonical way to build reliable AI agents. It prevents state loss and ensures tool calls are resilient to failure.
-   **`WorkflowChatTransport` for Reliable Streaming**: For chat applications, this transport for the AI SDK ensures that message streams can survive network interruptions or page reloads.
-   **`getWritable()` for Real-time Feedback**: Use this to stream data (progress updates, logs, AI tokens) from your workflow back to the client. It's key for creating responsive UIs for long-running processes.

---

## 5. Deployment & Configuration ("Worlds")

---

## 6. Example-Driven Playbooks
The fastest way to internalize these lessons is to study the living examples under `.workflow_docs/examples/`. The accompanying [`examples/LESSONS_LEARNED.md`](./examples/LESSONS_LEARNED.md) distills field observations into a checklist. Highlights:

-   **RAG Agent** – Tool execution through steps, `DurableAgent` streaming, and strict separation of orchestration vs. execution.
-   **Flight Booking App** – Network-failure simulation, reconnection via `WorkflowChatTransport`, and mandatory `x-workflow-run-id` headers.
-   **AI SDK Workflow Patterns** – Canonical sequential/parallel/routing/orchestrator/evaluator loops with guardrails like iteration caps and `globalThis.fetch` overrides.
-   **Custom Adapter (Bun)** – `.well-known` handler wiring, `bun x workflow build`, and Bun-native runtime expectations.
-   **Next.js Starter** – Minimal baseline to validate your environment before layering on complexity.

Use the project that mirrors your use case as the implementation reference, then cross-check against this master document before shipping.

-   **"Worlds" Abstract the Environment**: A "World" is the adapter that connects your workflow code to the underlying infrastructure (storage, queuing, auth). This makes your code portable.
-   **Vercel World is Production-Ready**: For deploying on Vercel, the Vercel World is the fully managed, recommended solution. It requires minimal configuration.
-   **`withWorkflow()` is Mandatory for Next.js**: To integrate with Next.js, you *must* wrap your `next.config.ts` with `withWorkflow()`. This enables the crucial code transformation step. Forgetting this is a common source of errors.

This synthesized guide provides the core wisdom needed to effectively use the Workflow DevKit. Refer back to these lessons—and the example playbooks—to avoid common pitfalls and build truly durable applications.

