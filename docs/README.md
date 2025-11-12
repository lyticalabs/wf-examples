# README: The Workflow DevKit

Welcome to the comprehensive guide for the Workflow DevKit. This document serves as the primary entry point for developers and AI coding agents looking to understand, implement, and master the creation of durable, resilient, and complex workflows.

This guide is structured to provide a logical progression from getting started to deep diving into the core concepts and APIs.

---

## 1. Getting Started

For developers new to the Workflow DevKit, the best place to start is the **[Getting Started Guide](./getting-started/README.md)**.

This hands-on tutorial will walk you through:
-   Setting up a new Next.js project.
-   Installing the necessary packages.
-   Configuring your Next.js application to work with the devkit.
-   Creating and running your very first workflow, including a workflow function, step functions, and a route handler to trigger it.

By the end of the guide, you will have a practical, foundational understanding of how to build and execute workflows.

---

## 2. Core Concepts: The Foundations

Once you have your first workflow running, it's crucial to understand the foundational concepts that power the devkit. These principles are key to building robust and reliable applications.

Dive deeper into the **[Foundations Guide](./foundations/README.md)**.

-   **Workflows and Steps**: Learn the fundamental difference between workflow functions (`"use workflow"`), which orchestrate logic in a sandboxed environment, and step functions (`"use step"`), which execute tasks with full Node.js access. This separation is the cornerstone of the devkit's durability.
-   **Starting and Tracking**: Understand how to initiate workflows with `start()` and monitor their execution using the returned `Run` object.
-   **Control Flow**: Discover how to use standard JavaScript patterns like `async/await`, `Promise.all`, and `Promise.race` to create complex execution flows.
-   **Error Handling & Retries**: Learn about the automatic retry mechanism for steps and how to use `FatalError` and `RetryableError` for fine-grained control.
-   **External Interaction**: Grasp how to use Hooks and Webhooks to make your workflows interactive and responsive to external systems.
-   **Idempotency**: A critical concept for ensuring that retried steps don't produce unwanted duplicate side effects.
-   **Serialization**: Understand what data can be passed between workflows and steps.

---

## 3. How It Works: Under the Hood

For those who want to understand the mechanics behind the devkit, this section is for you. It explains how the `"use workflow"` and `"use step"` directives enable durable execution.

Explore the **[How It Works Guide](./how-it-works/README.md)**.

-   **Directives and Code Transformation**: See how the compiler transforms your code, separating orchestration from execution.
-   **Framework Integration**: Get a high-level view of how the devkit integrates with frameworks like Next.js.

---

## 4. API Reference

This is your detailed guide to every function, package, and module available in the devkit. It's an essential resource for day-to-day development.

Consult the **[API Reference](./api-reference/README.md)**.

-   **`workflow` Package**: The core primitives for building workflows (`sleep`, `createHook`, `fetch`, etc.).
-   **`workflow/api` Package**: The runtime API for controlling workflows from your application (`start`, `getRun`, `resumeHook`, etc.).
-   **`workflow/next` Package**: The `withWorkflow()` function for seamless Next.js integration.
-   **`@workflow/ai` Package**: Specialized tools like `DurableAgent` for building powerful AI-driven workflows.

---

## 5. Deploying Your Workflows

When you're ready to go to production, this guide explains the "World" concept, which is the key to running your workflows in different environments.

Read the **[Deploying Guide](./deploying/README.md)**.

-   **The "World" Concept**: Understand how this abstraction layer handles storage, queuing, and authentication.
-   **Vercel World**: The recommended, fully-managed solution for production deployments on Vercel.
-   **Custom Worlds**: Learn about creating your own `World` for other platforms, with Postgres as a reference implementation.

---

## 6. Observability & Debugging

Workflows are powerful, but you need visibility into their execution. This section covers the tools that help you monitor and debug your workflows.

Check out the **[Observability Guide](./observability/README.md)**.

-   **CLI and Web UI**: Learn how to use the powerful command-line and web-based tools to inspect runs, steps, and events.
-   **Connecting to Environments**: Discover how to connect the observability tools to both your local development server and your production deployments.

---

## 7. Troubleshooting

When you encounter issues, this guide provides solutions to common problems.

Refer to the **[Common Errors Guide](./errors/README.md)**.

-   Find solutions for issues related to sandboxed execution (`fetch` and Node.js modules), serialization, invalid configurations, and webhook handling.


