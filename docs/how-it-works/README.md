# README: How Workflows Work

Welcome to the guide on how the Workflow DevKit works. This document provides an in-depth overview of the core concepts that power the durable execution model of the workflow engine.

## Core Concepts

The key to understanding how workflows work is to understand the role of the `"use workflow"` and `"use step"` directives. These directives are not just markers; they are the foundation of the entire durable execution model.

### Directives and Code Transformation

-   **`"use workflow"` and `"use step"`**: These directives provide a clear, compile-time signal that a function has special execution semantics. This allows the compiler to perform the necessary transformations to enable durable execution.
-   **Code Transformation**: The directives trigger a code transformation process that separates the workflow's orchestration logic from its side effects. This allows the workflow to be replayed deterministically, while the steps are executed with full access to the Node.js runtime.

### Framework Integration

-   Integrating the Workflow DevKit with a framework involves two main components:
    1.  A **build-time step** to generate the workflow handler files.
    2.  A **runtime step** to expose these handlers as HTTP endpoints.

The documentation provides a clear example of how to do this with Bun, and the same principles can be applied to any JavaScript runtime.

### Why Directives?

-   The documentation provides a detailed explanation of why directives were chosen over other approaches, such as decorators or file-based conventions. The key takeaway is that directives provide a clear, unambiguous signal to both the compiler and the developer that a function has special execution semantics. This is crucial for ensuring the correctness and reliability of the workflow engine.


