# README: Common Workflow Errors

Welcome to the guide on common errors in the Workflow DevKit. This document provides an in-depth overview of the common issues that you may encounter when building and running workflows, and how to resolve them.

## Core Concepts

Workflows run in a sandboxed environment with specific constraints that are designed to ensure deterministic and replayable execution. Many common errors arise from a misunderstanding of these constraints. The key concepts to keep in mind are:

-   **Sandboxed Execution**: Workflow functions do not have direct access to the Node.js runtime or the global `fetch()` function.
-   **Determinism**: Workflow functions must be deterministic, meaning that they always produce the same output for the same input.
-   **Serialization**: All data passed between workflows and steps must be serializable.
-   **Build-time Transformation**: The Workflow DevKit uses a build-time transformation to process your workflow code.

---

## Common Errors and Solutions

### `fetch-in-workflow`

-   **Problem**: You cannot use the global `fetch()` function directly in a workflow function.
-   **Solution**: Use the `fetch` step function provided by the `workflow` package. For libraries that use `fetch()` internally, you can make it available by assigning `globalThis.fetch = fetch` at the beginning of your workflow.

### `node-js-module-in-workflow`

-   **Problem**: You cannot use Node.js core modules like `fs`, `http`, or `crypto` directly in a workflow function.
-   **Solution**: Move any code that relies on these modules into a separate step function, which has full access to the Node.js runtime.

### `serialization-failed`

-   **Problem**: You are trying to pass non-serializable data (e.g., functions, class instances) between a workflow and a step.
-   **Solution**: Pass plain data and reconstruct any necessary objects or logic within the step or workflow.

### `start-invalid-workflow-function`

-   **Problem**: The `start()` function is being called with an invalid workflow function.
-   **Solution**: Ensure that the function has the `"use workflow"` directive, that your `next.config.ts` is wrapped with `withWorkflow()`, and that you are importing the correct function.

### `webhook-invalid-respond-with-value`

-   **Problem**: You are providing an invalid value for the `respondWith` option when creating a webhook.
-   **Solution**: The `respondWith` option can only be set to `"manual"`, a `Response` object, or be left `undefined` for a default `202 Accepted` response.

### `webhook-response-not-sent`

-   **Problem**: A webhook is configured with `respondWith: "manual"`, but the workflow does not send a response.
-   **Solution**: Ensure that all code paths, including error conditions, send a response using `request.respondWith()` when using manual response mode.


